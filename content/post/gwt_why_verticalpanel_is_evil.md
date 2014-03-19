{
 "disqus_url" : "http://trishagee.github.io/post/gwt_why_verticalpanel_is_evil/",
 "disqus_title" : "GWT: Why VerticalPanel is Evil",
 "Title": "GWT: Why VerticalPanel is Evil",
 "Pubdate": "2011-01-21",
 "Slug": "gwt_why_verticalpanel_is_evil",
 "Section": "post"
}
At <a href="http://www.lmaxtrader.co.uk/about-lmax">LMAX</a> we adopted <a href="http://code.google.com/webtoolkit/gettingstarted.html">Google Web Toolkit</a> pretty early on. &nbsp;One of the motivations for using it was so we only had to worry about recruiting Java guys, and then we could all work on every part of the application including the web UI. &nbsp;Sure, you can learn a bunch of different skills if you want to, but it reduced context-switching and kept the skill set we were hiring for to a nice short list.<br /><div><br /></div><div>The problem is that GWT does a very nice job of pretending to be Java whilst actually compiling down to HTML and JavaScript. &nbsp;If you don't have some understanding of the end result (the <a href="http://www.w3.org/DOM/">DOM</a> the browser is going to be rendering) it's going to be hard to get the performance you need from a <a href="http://www.lmaxtrader.co.uk/trading-platforms/web-platform">low-latency trading application</a>.</div><div><br /></div><div>My number one bug-bear with GWT is <a href="http://google-web-toolkit.googlecode.com/svn/javadoc/2.1/com/google/gwt/user/client/ui/VerticalPanel.html">VerticalPanel</a>. &nbsp;To the uninitiated developer, this seems like the sort of thing that will be useful everywhere. &nbsp;You often want stuff stacked on top of each other - think menus, lists, the layout of a dialog. &nbsp;What is not obvious is that it uses tables for layout under the covers, and I've mentioned in the past that <a href="http://mechanitis.blogspot.com/2011/01/css-for-developers-horizontal-layout.html">Tables Should Not Be Used For Layout</a>.</div><div><br /></div><div>A much less obvious way of getting the same result with (usually) no extra effort is to use <a href="http://google-web-toolkit.googlecode.com/svn/javadoc/2.1/com/google/gwt/user/client/ui/FlowPanel.html">FlowPanel</a>. &nbsp;This is rendered as a div, and most of the time the elements that get inserted into it will render in a vertical stack.<br /><br /></div><div><b>VerticalPanel Code</b><br /><blockquote><code>VerticalPanel panel = new VerticalPanel();<br />panel.add(/* your widget */);<br />panel.add(/* your second widget */);<br /></code></blockquote></div><div><b>VerticalPanel Rendered As HTML</b></div><div><blockquote><pre><code>&lt;table&gt;<br />  &lt;tbody&gt;<br />    &lt;tr&gt;<br />      &lt;td&gt;<br />        &lt;!-- your widget here --&gt;<br />      &lt;/td&gt;<br />     &lt;tr&gt;<br />    &lt;tr&gt;<br />      &lt;td&gt;<br />        &lt;!-- your second widget here --&gt;<br />      &lt;/td&gt;<br />     &lt;tr&gt;<br />  &lt;/tbody&gt;<br />&lt;table&gt;<br /></code></pre></blockquote></div><div><b>FlowPanel Code</b><br /><blockquote><code>FlowPanel panel = new FlowPanel();<br />panel.add(/* your widget */);<br />panel.add(/* your second widget */);</code></blockquote></div><div><b>FlowPanel Rendered As HTML</b></div><div><blockquote><pre><code>&lt;div&gt;<br />  &lt;!-- your widget here --&gt;<br />  &lt;!-- your second widget here --&gt;<br />&lt;/div&gt;<br /></code></pre></blockquote>You can see that the DOM generated for a very similar-looking 3 lines of code is much much smaller for <code>FlowPanel</code>.<br /><br /><span class="Apple-style-span" style="font-size: large;">Who Cares?</span><br />Right, but we're only talking about a few more elements, and browsers are pretty smart about optimising these things. &nbsp;Right?<br /><br />Maybe. &nbsp;But if you use <code>VerticalPanel</code> for all your containers, for every box which needs to be a slightly different colour, for every place you want to change the alignment slightly, things get very big very fast. &nbsp;This is an example of real code from an early prototype, where we had several nested panels (not unheard of if you've got a complex dialog box with lots of elements in it. &nbsp;Like, say, a deal ticket). &nbsp;And I've stripped out a lot of the table attributes that made this even more heinous:</div><br /><blockquote><pre><code>&lt;table&gt;<br />  &lt;tbody&gt;<br />    &lt;tr&gt;<br />      &lt;td align="left"&gt;<br />        &lt;table id="panel1"&gt;<br />          &lt;tbody&gt;<br />            &lt;tr&gt;<br />              &lt;td align="left" style="vertical-align: top;"&gt;<br />                &lt;table class="orders-input"&gt;<br />                  &lt;tbody&gt;<br />                    &lt;tr&gt;<br />                      &lt;td align="left"&gt;<br />                        &lt;table class="row"&gt;<br />                          &lt;tbody&gt;<br />                            &lt;tr&gt;<br />                              &lt;td align="left"&gt;<br />                                &lt;table id="container"&gt;<br />                                  &lt;tbody&gt;<br />                                    &lt;tr&gt;<br />                                      &lt;table id="panel2"&gt;<br />                                        &lt;tbody&gt;<br />                                          &lt;tr&gt;<br />                                            &lt;td align="left"&gt;<br />                                              &lt;table class="controls"&gt;<br />                                                &lt;tbody&gt;<br />                                                  &lt;tr&gt;<br />                                                    &lt;td align="left"&gt;<br />                                                      &lt;!-- widget --&gt;<br /></code></pre></blockquote><br />For every <code>table</code> element and associated elements (<code>tbody</code>, <code>tr</code>, <code>td</code>), you would get a single div element instead if you simply replace every instance of <code>VerticalPanel</code> in this stack with a <code>FlowPanel</code>.<br /><br /><blockquote><pre><code>&lt;div&gt;<br />  &lt;div id="panel1"&gt;<br />    &lt;div class="orders-input"&gt;<br />      &lt;div class="row"&gt;<br />        &lt;div id="container"&gt;<br />          &lt;div id="panel2"&gt;<br />            &lt;div class="controls"&gt;<br />              &lt;!-- widget --&gt;<br /></code></pre></blockquote><br />See?  Much nicer.<br /><br />This is exactly what we did do, and we saw a&nbsp;noticeable&nbsp;speed improvement across all browsers -&nbsp;noticeable&nbsp;to a real user, not just some millisecond improvement on a performance test. &nbsp;Mind you, users' brains are amazing things and your system has to react in <a href="http://www.useit.com/papers/responsetime.html">less than 0.1 seconds for a user to perceive it as instantaneous</a>. &nbsp;So even in a browser, every millisecond counts.<br /><br />In addition to improved performance, you get a nice bonus: now the layout is no longer controlled by tables, you can really easily shove stuff around and make things look pretty with the clever use of <a href="http://mechanitis.blogspot.com/search/label/css">CSS</a>. &nbsp;If you're really lucky, you can chuck that stuff over to your designers and not have to do another GWT compile when someone wants to move things 3 pixels to the left. &nbsp;Which they will.