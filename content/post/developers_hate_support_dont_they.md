{
 "disqus_url" : "http://trishagee.github.io/post/developers_hate_support_dont_they/",
 "disqus_title" : "Developers hate support, don't they?",
 "Title": "Developers hate support, don't they?",
 "Pubdate": "2013-07-05",
 "Slug": "developers_hate_support_dont_they",
 "Section": "post"
}
<table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;"><a href="http://3.bp.blogspot.com/-qUzWj04nHbo/Udbh8WSGszI/AAAAAAAALmg/n20nSELS6-U/s1600/Dublin.jpg" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="176" src="http://3.bp.blogspot.com/-qUzWj04nHbo/Udbh8WSGszI/AAAAAAAALmg/n20nSELS6-U/s640/Dublin.jpg" width="640" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">This is Dublin. &nbsp;Honest.</td></tr></tbody></table>I'm at the end of my first official week doing support for <a href="http://www.10gen.com/">10gen</a>. &nbsp;My major achievements are:<br /><ul><li>Learning how to work the coffee machine in the Dublin office. &nbsp;It's taken me a week to get it, but now I can understand the machine's needs. &nbsp;Even if my coffee did taste a bit of cleaning fluid this morning.</li><li>Navigating around Dublin - I led the way to the pub, followed by two people who live here. Turns out I know the most efficient routes between work venues and pubs, even in a town that I've never been to before.</li><li>Closing all outstanding&nbsp;<a href="https://github.com/mongodb/mongo-java-driver/pulls">Java driver pull requests</a>, except for the one we want to merge but needs to be updated. &nbsp;This is a massive win for us, now we can actually stay on top of them instead of wondering which are valid and which ones we're actively ignoring. &nbsp;I hope the CTO isn't peeved I closed one of his from two years ago.</li><li>I got my highest scoring day on <a href="http://stackoverflow.com/">StackOverflow</a> yesterday, receiving a "whopping" 67 points in one day. &nbsp;Be nice, I'm quite new to SO - despite being on there for over two years I'm really only just starting to feel comfortable there. &nbsp;One day I might actually <i>ask</i> a question.</li></ul><div>In all seriousness though, I learnt a LOT this week. &nbsp;I've been with 10gen for about 9 months now, so although I feel like I should be a fully fledged member of the team there's still a lot I don't know about. &nbsp;In particular, as I hadn't used MongoDB before working here, and as I'm head-down on delivering the new Java driver (more to come on that later, I promise), I don't see a lot of how people actually use the database.</div><div><br /></div><div>I've been lucky because this wasn't a heavy week for customer support, so I've been available to pick up "free" support - basically take a look at questions people are asking on StackOverflow and the MongoDB Google Groups and see if there's anything I can answer. &nbsp;Obviously I focussed on the Java side as this is the area I'm most comfortable (and there are only a few of us to answer those questions, and plenty of others to pick up more general questions). &nbsp;</div><div><br /></div><div>So here are my Lessons Learnt:</div><br /><div><b>Customers want to be heard</b></div><div><div>Responsiveness is almost more important to (paying) customers than detailed answers. &nbsp;They want to know that you've seen their problem, and you're on it. &nbsp;So sometimes it's best to answer a problem with a question or questions, asking for clarification on their situation and explaining any assumptions you have. &nbsp;It turns out that writing that long and detailed explanation of the steps they need to take isn't really necessary when you've figured out what they're really trying to do and response with "this is going to require production downtime". Suddenly it's not as urgent for them to fix this&nbsp;<i>right now</i>.</div><div><br /></div></div><div><b>The Java Ecosystem is alive and well. &nbsp;In fact, it's a monster...</b></div><div>There really are a <a href="http://docs.mongodb.org/ecosystem/drivers/java/">remarkable number of libraries/third party apps</a> that people are using on top of our <a href="http://docs.mongodb.org/ecosystem/tutorial/getting-started-with-java-driver/#getting-started-with-java-driver">basic Java driver</a>. &nbsp;This week, I've been trouble-shooting people using <a href="https://github.com/mongodb/morphia?source=c#morphia">Morphia</a>, <a href="http://www.springsource.org/spring-data/mongodb">Spring Data</a>, <a href="http://jongo.org/">Jongo</a>, <a href="http://grails.org/plugin/mongodb">Grails GORM</a>, as well as a lot of people who are using the driver directly. &nbsp;I've learnt a lot about installing and using all these things, as I've had to do that to reproduce people's issues and suggest solutions<sup><span style="font-size: x-small;">1</span></sup>. &nbsp;I've learnt that some of those things make life quite a lot easier, especially for the happy path of Java developers who simply want to save Java pojos into the DB and query for them afterwards. <br /><br />I've also learnt that querying is quite inconsistent across all the libraries, and I'd say the main problem that users have is turning an understandable query from the shell into something that the library they're using understands.<br /><br />Also, Dates get people every time, particularly in Java.<br /><br /><b>Where is the problem?</b></div><div>Related to the previous point, when a query returns nothing it's difficult to work out: if you're using the library incorrectly; if the Java driver doesn't support various options; or if the database isn't doing what you expect it to. &nbsp;More often than not the problem is not understanding how to use the tools (and the onus is on us, the library developers, to make it as easy and unsurprising as possible for developers), but sometimes it's a bug. &nbsp;Tracking down the root of the issue is important, because if it's a bug we should log it in the correct place, and if it's working as designed it suggests a lack of documentation or possibly a design flaw.</div><div></div><br /><div><b>Having people to help you is dead important</b></div><div>I could have done this from home, from the London office, or &nbsp;even from the beach if I'd wanted to. However, I opted to come to our Dublin office where we have our EMEA support, because I knew that alone I'd try and dodge the work. &nbsp;Not because I don't want to do it, but because I don't know our processes, I don't know if we have a knowledge base I can use, I don't know if my answers are correct, and so on and so on. &nbsp;When you're uncertain, sometimes the easiest option is to run away. But when you're embedded in the team that does this every day, you can ask the stupid questions and get help rather than sit and feel stupid. &nbsp;</div><div><br /></div><div>It's also nice to be part of a daily standup so you can hear what other people are up to, and it puts a (good) subtle pressure on you to do something so you have something to report.</div><div><br /></div><div><b>What I like about support at 10gen</b></div><div>I've done support before. &nbsp;In fact, during my last year at LMAX I worked out I spent the same amount of time on the production support team as I did working on a team delivering new features. &nbsp;But since I've never worked for a product firm before, I haven't done this sort of support. &nbsp;10gen makes its money by selling support contracts, so not only is it important to keep the SLAs with the paying customers, but it's also important to provide excellent quality support for them - with any luck they'll keep paying. &nbsp;It's also important for us to support those who don't pay - it's kinda like a teaser of the great quality they'd get if they paid us.</div><div><br /></div><div>So the support organisation here is&nbsp;absolutely&nbsp;key to our bottom line.</div><div><br /></div><div>The driver developers (of which I am one) are "strongly encouraged" to do a week of support every three months. &nbsp;We used to do days here and there, but blocking out a whole week to be part of the team, to be excused from your day job, and to leave your e-mail (and sometimes meetings) alone because you're busy doing support, works really well. &nbsp;I've felt very focussed on the support role during this week, and I've been motivated to do a good job. &nbsp;If I had been seconded to the team for a period of weeks, I would have dreaded the whole thing and have plodded along doing my time until my escape. Alternatively, doing it for a day at a time the support issues leak into the day job and the day job is hard to put down during your support hours.</div><div><br /></div><div>I've learnt a lot this week. &nbsp;I have been lucky, I've had fairly straightforward issues to address and it hasn't been a busy week. &nbsp;But next time I see the support week looming in my calendar, I won't fear it as much. &nbsp;I'll probably do the next one from home, but my week here in Dublin has prepared me for what's in store. &nbsp;Most importantly, I've got to know the people who are part of my team here, so I'll be more comfortable asking the stupid questions.</div><div><br /></div><div><b>In summary</b></div><div><ul><li>Doing support is so important for developers. &nbsp;Getting an understanding of what your users are doing and what their pain points are can really help drive your design and your architecture, and can really motivate you to fix that stupid bug or write that overdue tutorial.</li><li>Developers and support techies can learn off each other - I've learnt a LOT off the guys here, but I've also been able to answer a few questions about Java in general and the driver in particular.</li><li>Scheduling time in support for developers is a very tricky balance, and probably needs to be experimented with a bit before a company finds something that works for them. &nbsp;</li></ul></div><div>Although I'm never really going to <i>love</i> being on support, I still like being encouraged to work on support regularly - it's been so important for my understanding of our product and of our users.</div><div><br /></div><div><sup>1</sup><span style="font-size: x-small;"> I found Grails BY FAR the most difficult to get started with - all I wanted was to write a unit test to prove the issue, and I had to not only create a whole application using the grails command line, but I had to install a whole host of plugins and uninstall all the stuff for hibernate that gets put in there magically. &nbsp;I never did find the solution to the Grails problem I was looking at.</span></div>