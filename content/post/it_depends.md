{
 "disqus_url" : "http://trishagee.github.io/post/it_depends/",
 "disqus_title" : "It Depends",
 "Title": "It Depends",
 "Pubdate": "2013-03-18",
 "Slug": "it_depends",
 "Section": "post"
}
Don't you hate it when you ask a perfectly good question, and someone comes back with the answer "it depends"?<br /><br />It's so frustrating to think that in a world of ones and zeros, people can't give absolute answers and you can't rely on "best practice".<br /><br />It's an answer I've given so many times, especially when someone asks about performance. &nbsp;Well, I've had my&nbsp;comeuppance. &nbsp;The entire exercise of designing the new Java driver for <a href="http://www.mongodb.org/">MongoDB</a> has been nothing but a series of questions where the answer is "it depends":<br /><ul><li>Which Java version are our users, um, using?</li><li>Do people want an asynchronous driver?</li><li>How will they want to work with async?</li><li>Will they want to use async and synchronous method calls from the same application?</li><li>Do people typically use the Java driver directly, or do they use something that wraps it, like <a href="https://code.google.com/p/morphia/">Morphia</a> or <a href="http://www.springsource.org/spring-data">Spring Data</a>?</li><li>What's most important for users in terms of performance? &nbsp;Throughput? Latency? Consistent GC profile? Something else?</li><li>What sorts of operations are our users doing?</li><li>Do people usually update their driver and the server version at the same time?</li><li>Is it easier for them to update their driver version than their server version?</li><li>Do they use (or will they need) custom encoders and decoders?</li><li>When should we deprecate? &nbsp;When should we remove deprecated methods?</li></ul>...and so on, and so forth.<br /><br />It's such a change from the sort of development I'm used to: "the business" (a business analyst, a customer, a business owner) comes to you with a requirement, you ask a bunch of questions, preferably explaining the trade-offs that come with decisions or approaches, and then you and the team come up with a design and implement it. &nbsp;If you're agile, this is all done in a nice, iterative fashion, which hopefully leads to "the business" being happy, or at the very least to another series of stories/requirements to work on.<br /><br />The problem is that working on a library, particularly an open source library, is a completely different thing. &nbsp;We don't even know who our users are. &nbsp;This statement is true for pretty much any web application, of course, but there at least you can (if you choose) use tools like analytics and <a href="http://en.wikipedia.org/wiki/A/B_testing">A/B testing</a> to figure out what works for your users and what doesn't.<br /><br />When your library is used for free by all kinds of different teams and companies, including organisations behind closed doors, you have no idea what's being used, what works, what people like, what people don't like. &nbsp;The most visible feedback you have is when you see blog posts telling everyone how bad your product is.<br /><br />This makes the design exercise VERY difficult. &nbsp;Take performance for example. &nbsp;Having come from a high performance, low latency background, I'm desperate to have a very extensive suite of automated performance tests (and we do already have some). &nbsp;But how do I design those, when I don't know:<br /><ul><li>What operations are typical for our users</li><li>Whether our users care more about latency or throughput, or mean latency vs the long tail, or GC pauses, etc</li><li>How much data customers tend to punt around</li><li>What the hardware or network topology looks like?</li></ul><br />The number one lesson you learn when performance testing is to make your test environment as similar to production as possible. &nbsp;How can we do that for all our customers?<br /><br />Well, we can't. &nbsp;Of course.<br /><br />What we can do is offer an easy way for our users to test it for themselves, with their own data, their own hardware, their own use-cases. &nbsp;If we can provide some sort of hook into standard metrics, we could get users to plug into that and do what they needed. &nbsp;In theory, as we get more examples of these standard metrics from a range of users, it will be easier for us to help them diagnose problems. <br /><br />What I discovered thinking about this problem is that I was asking the wrong question - it's not "how do we test this?" but "how do we make it as easy as possible for users to test this in a production-like environment?".<br /><br />My biggest headache has been backwards compatibility. &nbsp;I've worked on plenty of systems where we've provided an API which has to be maintained in a friendly way for those who use it. &nbsp;That's tough enough - you have to be careful to only add methods, not to change signatures or remove them altogether. &nbsp;But when your system is not simply an API to code against, but a library that runs within other people's systems, this problem is even harder. &nbsp;<a href="http://qconlondon.com/london-2013/presentation/Parallel%20KEYNOTE:%208%20Lines%20of%20Code%20-%20Fleming%20Room%203rd%20Floor">Greg Young talked at QCon</a> about this problem from the developer's point of view - every piece of code in your system, even if it's a third party library, is your code. &nbsp;Because you're the one who'll get called at three in the morning if your system falls over with a ConcurrentModificationException in some third party data structure. <br /><br />So as library developers, we have to not only provide excellent quality, well tested code, but we also have to let our baby go off and run in strange environments. &nbsp;Ones that might not be running Oracle's Java 1.7, ones that might contain other libraries that could clash with our own. &nbsp;Have you ever looked at all the Maven dependencies in a large project? &nbsp;You can end up with conflicting versions of common libraries (e.g. logging or <a href="http://en.wikipedia.org/wiki/Dependency_injection">DI</a> frameworks) as every library you use pulls in dozens of libraries for itself.<br /><br />In our case then, we need to use as few dependencies as possible, and to write nice, clean, modern Java, whilst supporting older versions of Java. &nbsp;What's modern enough? &nbsp;We know that some large organisations take a loooong time to upgrade to the latest versions of Java. &nbsp;We currently support Java 5 and above, as 5 was a big enough change (and is old enough now) to be a good point to draw the line. &nbsp;But what about Java 7, with its shiny new <a href="http://docs.oracle.com/javase/7/docs/api/java/nio/channels/package-summary.html">asynchronous channels</a>? &nbsp;That would be awesome for a driver like ours, an application that exists solely to connect to some server somewhere. &nbsp;What about Java 8, with <a href="http://mechanitis.blogspot.co.uk/2012/11/java-8-introduction-to-lambdas-article.html">lambda goodness</a> and a very appealing <a href="http://cr.openjdk.java.net/~briangoetz/lambda/sotc3.html">Stream interface</a>, that supports (and encourages) a syntax that looks like it might work well for providing a fluent API for querying, I dunno, databases? &nbsp;How do we make the most out of advances in modern Java, without alienating our existing users?<br /><br />And, of course, I haven't even talked about actually changing the API. &nbsp;The existing Java driver doesn't even make use of generics. &nbsp;How can we change our API to provide a more modern-looking interface, without either forcing all our users to make massive changes to their applications (and for what? &nbsp;Their code already works), or adding so many new classes and methods that it becomes very difficult for new users to work out the Best Practice way of interacting with our driver?<br /><br />So, what can we do?<br /><ul><li>Firstly we have to figure out which questions we have and what possible solutions exist.</li><li>Then we have to weigh up the pros and cons of each of the possible solutions.</li><li>Ideally we'd get feedback early and often from our users, from the community, about the approaches we're taking.</li><li>Development would happen in parallel, in a nice, agile, way, to bring the best possible solution for everyone.</li></ul><br />What this all really means, though, is that the Shiny New Java Driver™ is not ready right now, and will not be ready immediately, despite the fact that we've already spent some time on its development, and considered all of those questions and more. &nbsp;Right now, we're starting to get feedback from the community - from users, and from committers (or people who would like to be committers). &nbsp;Which means that I get to to go to more conferences and user groups, and talk about our problems when designing the new driver. &nbsp;I'm hoping to get two things out of this, apart from more air miles:<br /><ol><li>Feedback from the community about our assumptions and the direction we're taking.</li><li>Present to the development community some of the lessons we've learnt/are learning, in the hope that you can use them when approaching the design of your own applications.</li></ol><div>&lt;gratuitous-conference-plug&gt;You've already seen some of these <a href="http://mechanitis.blogspot.co.uk/2013/03/upcoming-events.html">upcoming events</a>. &nbsp;But in case you haven't, <a href="http://www.meetup.com/Londonjavacommunity/events/109032992/">this Thursday I'll be presenting at Skillsmatter</a> on how we approached this design problem, and <a href="http://www.devoxx.com/display/UK13/What+do+you+mean%2C+backwards+compatibility">again at DevoxxUK next week</a>.</div><div><br /></div><div>If you're more interested in everything MongoDB, and want to get a much better look at what it is, how it works, how to design for it, then come to <a href="http://www.10gen.com/events/mongodb-london-2013">MongoDB London</a>, where I am one of numerous presenters, all going into MongoDB specifics.&lt;/gratuitous-conference-plug&gt;</div><div><br /></div><div>So... I'm afraid to say that even after this long post, even after bemoaning my own experiences of hearing "it depends", I still don't have an answer for you.</div><div><br /></div><div>But maybe I do. &nbsp;</div><div><br /></div><div>"It Depends" means "you need to get more information in order to answer that question". &nbsp;And it's our job as developers to ask the right questions to gather that information. &nbsp;If the answer is "it depends", you're not asking the right question yet, or you're not asking the right people. &nbsp;So dig down, find out why you can't answer the original question, and start iterating through your design process until you have answers that you can act upon.</div><div><br />Easy. &nbsp;Right...?</div>