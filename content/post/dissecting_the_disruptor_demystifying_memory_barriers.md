{
 "disqus_url" : "http://trishagee.github.io/post/dissecting_the_disruptor_demystifying_memory_barriers/",
 "disqus_title" : "Dissecting the Disruptor: Demystifying Memory Barriers",
 "Title": "Dissecting the Disruptor: Demystifying Memory Barriers",
 "Pubdate": "2011-08-07",
 "Slug": "dissecting_the_disruptor_demystifying_memory_barriers",
 "Section": "post"
}
My recent slow-down in posting is because I've been trying to write a post explaining <a href="http://en.wikipedia.org/wiki/Memory_barrier">memory barriers</a> and their applicability in <a href="http://code.google.com/p/disruptor">the Disruptor</a>.  The problem is, no matter how much I read and no matter how many times I ask the ever-patient <a href="http://mechanical-sympathy.blogspot.com/">Martin</a> and <a href="http://mikes-tech.blogspot.com/">Mike</a> questions trying to clarify some point, I just don't intuitively grasp the subject.  I guess I don't have the deep background knowledge required to fully understand.<br /><br />So, rather than make an idiot of myself trying to explain something I don't really get, I'm going to try and cover, at an abstract / massive-simplification level, what I do understand in the area. &nbsp;Martin has written a post&nbsp;<a href="http://mechanical-sympathy.blogspot.com/2011/07/memory-barriersfences.html">going into memory barriers</a>&nbsp;in some detail, so hopefully I can get away with skimming the subject.<br /><br />Disclaimer: any errors in the explanation are completely my own, and no reflection on the implementation of the Disruptor or on the <a href="http://www.lmaxtrader.co.uk/">LMAX </a>guys who actually do know about this stuff.<br /><br /><b>What's the point?</b><br />My main aim in this series of blog posts is to explain how the Disruptor works and, to a slightly lesser extent, why.  In theory I should be able to provide a bridge between the code and <a href="http://disruptor.googlecode.com/files/Disruptor-1.0.pdf">the technical paper</a> by talking about it from the point of view of a developer who might want to use it.<br /><br />The paper mentioned memory barriers, and I wanted to understand what they were, and how they apply.<br /><br /><b>What's a Memory Barrier?</b><br />It's a CPU instruction. &nbsp;Yes, once again, we're thinking about CPU-level stuff in order to get the performance we need (Martin's famous Mechanical Sympathy). &nbsp;Basically it's an instruction to a) ensure the order in which certain operations are executed and b) influence visibility of some data (which might be the result of executing some instruction).<br /><br />Compilers and CPUs can re-order instructions, provided the end result is the same, to try and optimise performance. &nbsp;Inserting a memory barrier tells the CPU and the compiler that what happened before that command needs to stay before that command, and what happens after needs to stay after. &nbsp;All similarities to a trip to Vegas are entirely in your own mind.<br /><br /><div class="separator" style="clear: both; text-align: center;"><a href="http://2.bp.blogspot.com/-wae8jx9Ehuw/Tjg5oFT5M7I/AAAAAAAAIJI/J00e1Fy42DU/s1600/MemoryBarrier.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-wae8jx9Ehuw/Tjg5oFT5M7I/AAAAAAAAIJI/J00e1Fy42DU/s1600/MemoryBarrier.png" /></a></div><br />The other thing a memory barrier does is force an update of the various CPU caches - for example, a write barrier will flush all the data that was written before the barrier out to cache, therefore any other thread that tries to read that data will get the most up-to-date version regardless of which core or which socket it might be executing by.<br /><br /><b>What's this got to do with Java?</b><br />Now I know what you're thinking - this isn't assembler. &nbsp;It's Java. <br /><br /><span class="Apple-style-span">The magic incantation here is the word&nbsp;<code>volatile</code>&nbsp;(something I felt was never clearly explained in the Java certification). &nbsp;If your field is&nbsp;</span><span class="Apple-style-span" style="font-family: monospace;">volatile</span><span class="Apple-style-span">, the Java Memory Model inserts a write barrier instruction after you write to it, and a read barrier instruction before you read from it.</span><br /><span class="Apple-style-span"><br /></span><br /><div class="separator" style="clear: both; text-align: center;"><a href="http://3.bp.blogspot.com/-mdQ0VfzF_XM/TjhOOM4PBEI/AAAAAAAAIJQ/K25fNMkKufU/s1600/MemoryBarrierWrite.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-mdQ0VfzF_XM/TjhOOM4PBEI/AAAAAAAAIJQ/K25fNMkKufU/s1600/MemoryBarrierWrite.png" /></a></div><span class="Apple-style-span"></span><br />This means if you write to a volatile field, you know that:<br /><ol><li>Any thread accessing that field after the point at which you wrote to it will get the updated value&nbsp;</li><li>Anything you did before you wrote that field is guaranteed to have happened and any updated data values will also be visible, because the memory barrier flushed all earlier writes to the cache.</li></ol><div><b>Example please!</b></div><div>So glad you asked. &nbsp;It's about time I started drawing doughnuts again.</div><div><br /></div><div>The&nbsp;<a href="http://code.google.com/p/disruptor/source/browse/trunk/code/src/main/com/lmax/disruptor/RingBuffer.java">RingBuffer</a>&nbsp;<code>cursor</code> is one of these magic volatile thingies, and it's one of the reasons we can get away with implementing the Disruptor without locking.</div><div><br /></div><div class="separator" style="clear: both; text-align: center;"><a href="http://2.bp.blogspot.com/-_JxCXwReRgA/TjhGfFrokHI/AAAAAAAAIJM/i_VC0M_K5hw/s1600/BarriersWriteExample.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="226" src="http://2.bp.blogspot.com/-_JxCXwReRgA/TjhGfFrokHI/AAAAAAAAIJM/i_VC0M_K5hw/s400/BarriersWriteExample.png" width="400" /></a></div><div><br /></div><div>The Producer will obtain the next <a href="http://code.google.com/p/disruptor/source/browse/trunk/code/src/main/com/lmax/disruptor/AbstractEntry.java?spec=svn109&amp;r=201">Entry</a> (or batch of them) and do whatever it needs to do to the entries, updating them with whatever values it wants to place in there. &nbsp;<a href="http://mechanitis.blogspot.com/2011/07/dissecting-disruptor-writing-to-ring.html">As you know</a>, at the end of all the changes the producer calls the commit method on the ring buffer, which updates the sequence number. &nbsp;This write of the volatile field (<code>cursor</code>) creates a memory barrier which ultimately brings all the caches up to date (or at least invalidates them accordingly). &nbsp;</div><div><br /></div><div>At this point, the consumers can get the updated sequence number (8), and because the memory barrier also guarantees the ordering of the instructions that happened before then, the consumers can be confident that all changes the producer did to to the <a href="http://code.google.com/p/disruptor/source/browse/trunk/code/src/main/com/lmax/disruptor/AbstractEntry.java?spec=svn109&amp;r=201">Entry</a> at position 7 are also available.</div><div><br /></div><div><b>...and on the Consumer side?</b></div><div>The sequence number on the Consumer is volatile, and read by a number of external objects - other <a href="http://mechanitis.blogspot.com/2011/07/dissecting-disruptor-wiring-up.html">downstream</a> consumers might be tracking this consumer<a href="http://mechanitis.blogspot.com/2011/07/dissecting-disruptor-wiring-up.html">,</a>&nbsp;and&nbsp;the <a href="http://code.google.com/p/disruptor/source/browse/trunk/code/src/main/com/lmax/disruptor/ProducerBarrier.java?spec=svn109&amp;r=201">ProducerBarrier</a>/<a href="http://code.google.com/p/disruptor/source/browse/trunk/code/src/main/com/lmax/disruptor/RingBuffer.java?spec=svn109&amp;r=242">RingBuffer</a> (depending on whether you're looking at older or newer code) tracks it to make sure the the ring doesn't wrap.<br /><br /><div class="separator" style="clear: both; text-align: center;"></div><div class="separator" style="clear: both; text-align: center;"><a href="http://2.bp.blogspot.com/-qoKYeSC2_OM/Tj7HG5U6RaI/AAAAAAAAIJc/hnLVu3EL-kE/s1600/MemoryBarrierReadExample.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-qoKYeSC2_OM/Tj7HG5U6RaI/AAAAAAAAIJc/hnLVu3EL-kE/s1600/MemoryBarrierReadExample.png" /></a></div><br />So, if your downstream consumer (C2) sees that an earlier consumer (C1) reaches number 12, when C2 reads entries up to 12 from the ring buffer it will get all updates C1 made to the entries before it updated its sequence number.<br /><br />Basically everything that happens after C2 gets the updated sequence number (shown in blue above) must occur after everything C1 did to the ring buffer before updating its sequence number (shown in black).<br /><br /><b>Impact on performance</b><br />Memory barriers, being another CPU-level instruction, don't have the same <a href="http://mechanitis.blogspot.com/2011/07/dissecting-disruptor-why-its-so-fast.html">cost as locks</a>&nbsp; - the kernel isn't interfering and arbitrating between multiple threads. &nbsp;But&nbsp;nothing comes for free. &nbsp;Memory barriers do have a cost - the compiler/CPU cannot re-order instructions, which could potentially lead to not using the CPU as efficiently as possible, and refreshing the caches obviously has a performance impact. &nbsp;So don't think that using volatile instead of locking will get you away scot free.<br /><br />You'll notice that the Disruptor implementation tries to read from and write to the sequence number as infrequently as possible. &nbsp;Every read or write of a <code>volatile</code> field is a relatively costly operation. However, recognising this also plays in quite nicely with batching behaviour - if you know you shouldn't read from or write to the sequences too frequently, it makes sense to grab a whole batch of Entries and process them before updating the sequence number, both on the Producer and Consumer side. Here's an example from <a href="http://code.google.com/p/disruptor/source/browse/trunk/code/src/main/com/lmax/disruptor/BatchConsumer.java?r=239">BatchConsumer</a>:<br /><br /><table id="src_table_0" style="-webkit-border-horizontal-spacing: 2px; -webkit-border-vertical-spacing: 2px; border-collapse: collapse; font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Lucida Console', monospace; font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px; white-space: pre;"><tbody style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><tr id="sl_svn239_121" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"></td></tr><tr id="sl_svn239_122" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; </span><span class="kwd" style="color: #000088;">long</span><span class="pln" style="color: black;"> nextSequence </span><span class="pun" style="color: #666600;">=</span><span class="pln" style="color: black;"> <b>sequence </b></span><span class="pun" style="color: #666600;">+</span><span class="pln" style="color: black;"> </span><span class="lit" style="color: #006666;">1</span><span class="pun" style="color: #666600;">;</span></td></tr><tr id="sl_svn239_123" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; </span><span class="kwd" style="color: #000088;">while</span><span class="pln" style="color: black;"> </span><span class="pun" style="color: #666600;">(</span><span class="pln" style="color: black;">running</span><span class="pun" style="color: #666600;">)</span></td></tr><tr id="sl_svn239_124" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; </span><span class="pun" style="color: #666600;">{</span></td></tr><tr id="sl_svn239_125" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; </span><span class="kwd" style="color: #000088;">try</span><span class="pln" style="color: black;"> </span></td></tr><tr id="sl_svn239_126" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; </span><span class="pun" style="color: #666600;">{</span></td></tr><tr id="sl_svn239_127" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="kwd" style="color: #000088;">final</span><span class="pln" style="color: black;"> </span><span class="kwd" style="color: #000088;">long</span><span class="pln" style="color: black;"> availableSequence </span><span class="pun" style="color: #666600;">=</span><span class="pln" style="color: black;"> consumerBarrier</span><span class="pun" style="color: #666600;">.</span><span class="pln" style="color: black;">waitFor</span><span class="pun" style="color: #666600;">(</span><span class="pln" style="color: black;">nextSequence</span><span class="pun" style="color: #666600;">);</span></td></tr><tr id="sl_svn239_128" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="kwd" style="color: #000088;">while</span><span class="pln" style="color: black;"> </span><span class="pun" style="color: #666600;">(</span><span class="pln" style="color: black;">nextSequence </span><span class="pun" style="color: #666600;">&lt;=</span><span class="pln" style="color: black;"> availableSequence</span><span class="pun" style="color: #666600;">)</span></td></tr><tr id="sl_svn239_129" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="pun" style="color: #666600;">{</span></td></tr><tr id="sl_svn239_130" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; entry </span><span class="pun" style="color: #666600;">=</span><span class="pln" style="color: black;"> consumerBarrier</span><span class="pun" style="color: #666600;">.</span><span class="pln" style="color: black;">getEntry</span><span class="pun" style="color: #666600;">(</span><span class="pln" style="color: black;">nextSequence</span><span class="pun" style="color: #666600;">);</span></td></tr><tr id="sl_svn239_131" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; handler</span><span class="pun" style="color: #666600;">.</span><span class="pln" style="color: black;">onAvailable</span><span class="pun" style="color: #666600;">(</span><span class="pln" style="color: black;">entry</span><span class="pun" style="color: #666600;">);</span></td></tr><tr id="sl_svn239_132" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; nextSequence</span><span class="pun" style="color: #666600;">++;</span></td></tr><tr id="sl_svn239_133" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="pun" style="color: #666600;">}</span></td></tr><tr id="sl_svn239_135" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; handler</span><span class="pun" style="color: #666600;">.</span><span class="pln" style="color: black;">onEndOfBatch</span><span class="pun" style="color: #666600;">();</span></td></tr><tr id="sl_svn239_136" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <b>sequence </b></span><span class="pun" style="color: #666600;">=</span><span class="pln" style="color: black;"> entry</span><span class="pun" style="color: #666600;">.</span><span class="pln" style="color: black;">getSequence</span><span class="pun" style="color: #666600;">();</span></td></tr><tr id="sl_svn239_137" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; </span><span class="pun" style="color: #666600;">}</span></td></tr><tr id="sl_svn239_138" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; </span><span class="pln"><span class="Apple-style-span" style="color: #000088;">...</span></span></td></tr><tr id="sl_svn239_142" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; </span><span class="kwd" style="color: #000088;">catch</span><span class="pln" style="color: black;"> </span><span class="pun" style="color: #666600;">(</span><span class="kwd" style="color: #000088;">final</span><span class="pln" style="color: black;"> </span><span class="typ" style="color: #660066;">Exception</span><span class="pln" style="color: black;"> ex</span><span class="pun" style="color: #666600;">)</span></td></tr><tr id="sl_svn239_143" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; </span><span class="pun" style="color: #666600;">{</span></td></tr><tr id="sl_svn239_144" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; exceptionHandler</span><span class="pun" style="color: #666600;">.</span><span class="pln" style="color: black;">handle</span><span class="pun" style="color: #666600;">(</span><span class="pln" style="color: black;">ex</span><span class="pun" style="color: #666600;">,</span><span class="pln" style="color: black;"> entry</span><span class="pun" style="color: #666600;">);</span></td></tr><tr id="sl_svn239_145" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <b>sequence </b></span><span class="pun" style="color: #666600;">=</span><span class="pln" style="color: black;"> entry</span><span class="pun" style="color: #666600;">.</span><span class="pln" style="color: black;">getSequence</span><span class="pun" style="color: #666600;">();</span></td></tr><tr id="sl_svn239_146" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; nextSequence </span><span class="pun" style="color: #666600;">=</span><span class="pln" style="color: black;"> entry</span><span class="pun" style="color: #666600;">.</span><span class="pln" style="color: black;">getSequence</span><span class="pun" style="color: #666600;">()</span><span class="pln" style="color: black;"> </span><span class="pun" style="color: #666600;">+</span><span class="pln" style="color: black;"> </span><span class="lit" style="color: #006666;">1</span><span class="pun" style="color: #666600;">;</span></td></tr><tr id="sl_svn239_147" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; &nbsp; &nbsp; </span><span class="pun" style="color: #666600;">}</span></td></tr><tr id="sl_svn239_148" style="margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;"><td class="source" style="font-size: 12px; margin-bottom: 0px; margin-left: 0px; margin-right: 0px; margin-top: 0px; padding-bottom: 0px; padding-left: 4px; padding-right: 0px; padding-top: 0px; vertical-align: top; white-space: pre-wrap;"><span class="pln" style="color: black;">&nbsp; &nbsp; </span><span class="pun" style="color: #666600;">}</span></td></tr></tbody></table><br />(You'll note this is the "old" code and naming conventions, because this is inline with my previous blog posts, I thought it was slightly less confusing than switching straight to the new conventions).<br /><br />In the code above, we use a local variable to increment during our loop over the entries the consumer is processing. &nbsp;This means we read from and write to the volatile sequence field (shown in bold) as infrequently as we can get away with.<br /><br /><b>In Summary</b><br />Memory barriers are CPU instructions that allow you to make certain assumptions about when data will be visible to other processes. &nbsp;In Java, you implement them with the <code>volatile</code> keyword. &nbsp;Using volatile means you don't necessarily have to add locks willy nilly, and will give you performance improvements over using them. &nbsp;However you need to think a little more carefully about your design, in particular how frequently you use volatile fields, and how frequently you read and write them.<br /><br /><br />PS Given that the <a href="http://mechanitis.blogspot.com/2011/08/disruptor-20-all-change-please.html">New World Order</a> in the Disruptor uses totally different naming conventions now to everything I've blogged about so far, I guess the next post is mapping the old world to the new one.</div><div></div>