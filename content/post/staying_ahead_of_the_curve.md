{
 "disqus_url" : "http://trishagee.github.io/post/staying_ahead_of_the_curve/",
 "disqus_title" : "Staying Ahead of the Curve",
 "Title": "Staying Ahead of the Curve",
 "Pubdate": "2013-02-20",
 "Keywords": ["jobs", "advice", "career"],
 "Tags": ["jobs", "advice", "career"],
 "Slug": "staying_ahead_of_the_curve",
 "Section": "post"
}
I had an interesting discussion last night at the <a href="http://www.meetup.com/Londonjavacommunity/">LJC</a> developer sessions, and
it's a topic that comes up again and again:

> How do I stay ahead of the curve?  There are so many technologies out there, and more coming along, I can't even keep up with Java,
> let alone the other JVM languages, HTML5, JavaScript frameworks, NoSQL, Big Data.... argh!

Technology, particularly development, seems to move at an ever-increasing pace.  Sure, the Internet makes it a lot easier for us to get access
to information than in the Olden Days, when people probably had to read papers and books, and physically meet up to share knowledge, but that just makes the sheer volume of information even more overwhelming.<br /><br />So how <i>do</i> you keep on top of all those technologies?<br /><br />You don't.<br /><br />You can't.  If you devoted yourself to learning the same way you did at university (pfff, well, theoretically you devoted yourself to learning...), you could still never master every technology out there, and every new language and framework that pops up daily.  Even people who pick a technology stack that's suitable for purpose (let's go with the old favourite Spring/Hibernate combo) can't read every blog post about those technologies and see every conference talk that was ever videoed.  To be the best even at Just Java, you'd have to be a master of concurrency, understand garbage collection, have read all revisions of <a href="http://www.amazon.com/gp/product/0321356683/ref=as_li_tf_tl?ie=UTF8&amp;camp=1789&amp;creative=9325&amp;creativeASIN=0321356683&amp;linkCode=as2&amp;tag=trissramb-20">Effective Java</a><img alt="" border="0" height="1" src="http://www.assoc-amazon.com/e/ir?t=trissramb-20&amp;l=as2&amp;o=1&amp;a=0321356683" style="border: none !important; margin: 0px !important;" width="1" />, know every detail of all versions of Java, including all the changes coming in <a href="http://jdk8.java.net/">Java 8</a>, be aware of all the <a href="http://jcp.org/en/jsr/stage?listBy=jsr">JSRs</a> in progress.  They'd have to have read about waterfall development, the <a href="http://www.amazon.com/gp/product/0201835959/ref=as_li_tf_tl?ie=UTF8&amp;camp=1789&amp;creative=9325&amp;creativeASIN=0201835959&amp;linkCode=as2&amp;tag=trissramb-20">Mythical Man-Month</a><img alt="" border="0" height="1" src="http://www.assoc-amazon.com/e/ir?t=trissramb-20&amp;l=as2&amp;o=1&amp;a=0201835959" style="border: none !important; margin: 0px !important;" width="1" />, <a href="http://www.amazon.com/gp/product/0321278658/ref=as_li_tf_tl?ie=UTF8&amp;camp=1789&amp;creative=9325&amp;creativeASIN=0321278658&amp;linkCode=as2&amp;tag=trissramb-20">XP</a><img alt="" border="0" height="1" src="http://www.assoc-amazon.com/e/ir?t=trissramb-20&amp;l=as2&amp;o=1&amp;a=0321278658" style="border: none !important; margin: 0px !important;" width="1" />, <a href="http://www.amazon.com/gp/product/0130676349/ref=as_li_tf_tl?ie=UTF8&amp;camp=1789&amp;creative=9325&amp;creativeASIN=0130676349&amp;linkCode=as2&amp;tag=trissramb-20">Scrum</a><img alt="" border="0" height="1" src="http://www.assoc-amazon.com/e/ir?t=trissramb-20&amp;l=as2&amp;o=1&amp;a=0130676349" style="border: none !important; margin: 0px !important;" width="1" />, Lean, <a href="http://www.infoq.com/presentations/Leaner-Programmer-Anarchy">Programmer Anarchy</a>, so that they could know they are working in the most effective way for the business and team they are in.<br /><br />All that as well as working 40 hours a week on the day job.<br /><br />So to expect to know the ins and out of all current (and maybe dated) technologies, and all upcoming ones - not knowing which are just fads and which are going to be the Next Big Thing - is impossible.

> But don't you ask candidates how they stay current when you interview them?

Yes I do. And actually it's their willingness to at least try, and their ability to filter out and select the things to investigate or be
aware of that interests me, not their deep understanding of Scala when they're working in a JEE environment (for example).

There are two reasons that I can think of to "stay ahead of the curve":

1. To be more effective in your job
1. To get your next job

If you're aiming for point one, it's a little easier to filter out the noise and focus on what's relevant.  In your place of work, there are going to be hard limits on new stuff you can use.  For example:

- Your systems guys will not allow new languages, even JVM ones, in a production environment.  In which case,
 you don't need to worry about learning them in any detail.
- Your company has paid a heavy subscription fee for their existing database, therefore they will not be trying out funky <a
href="http://mechanitis.blogspot.co.uk/2012/10/nosql-is-stupid-name.html">NoSQL</a> solutions.  Fine, you don't have to research them.
- You're working on a messaging system with no UI.  In which case, you can let the new JavaScript frameworks rise and fall without
worrying too much about them.
- You work for a consultancy that specialises in government work, and documentation is sacred.  So,
don't worry about going to a bunch of agile/lean conferences, you probably won't be able to sell it to your customers.

Now I'm not saying these circumstances apply to everyone.  And I'm not suggesting these are necessarily the best situations to be in.  But you can look at your current position and, if you intend to stay there, it might rule out a lot of the technology/process learning that's available.<br /><br />Point one suggests good places for research.  For example:

- You're using Spring dependency injection and you don't speak XML fluently.  So you might research Spring wired up via Java and <a
href="http://blog.springsource.org/2007/05/14/annotation-driven-dependency-injection-in-spring-21/">annotations</a>, or you might look at
<a href="http://code.google.com/p/google-guice/">Guice</a>, or you might do a bit more reading around good practises in XML, or tools you
can add to your IDE to make your life easier (<a href="http://www.eclipse.org/">Eclipse</a> and
<a href="http://www.jetbrains.com/idea/features/xml_editor.html">IntelliJ</a> both support XML refactoring).
- Your <a href="http://ant.apache.org/">Ant</a> scripts are killing you, and you don't know where your library jars should live.  You
could read a lot more about Ant, you might look into <a href="http://maven.apache.org/">Maven</a>,
<a href="http://ant.apache.org/ivy/">Ivy</a>, and <a href="http://www.gradle.org/">Gradle</a> (hint - gradle is awesome if you don't
like programming in XML).
- You spend all your time coercing objects into something <a href="http://www.hibernate.org/">Hibernate</a>-shaped,
and not actually delivering new functionality.  Maybe you could become a Hibernate guru instead of just poking at it like most of us do,
or you could investigate different persistence frameworks or mechanisms.

You get the idea.  If you feel pressured to keep learning and you're not looking for a new job, there's plenty you can be doing within the framework of your day job.  The best thing about this is that you might even be able to persuade your boss that you need to do some or all of this learning on work time, leaving you more time for your kids/spouse/drinking/XBox.

> I'm really much more motivated to learn skills to find that great new job

Point two is a bit more tricky.  When you're looking for a new job, it seems like every job description contains all technologies under the sun; it seems like interviewers expect you to be an expert in all sorts of different areas; it's impossible to tell which jobs are good and which are poor, so you apply for everything and try to learn everything to get to the interview.<br /><br />Now if you're already at the applying-for-a-new-job stage, you might not actually have time to learn everything under the sun.  And if you're still working at the current place and just looking around to see what's out there, you might not have time to train yourself up on all those great new JavaScript frameworks while doing the day job.

How on earth do you pick which things to focus on?

Well, it's surprisingly easy.  Just pick the ones that interest you.

> But what if I'm falling behind on technology X and it turns out to be The Next Big Thing?

Well, by the time it becomes the next big thing, you'll have heard enough about it to know whether or not you care  - either because it interests you or because it's so big you should care.  And by then, there will be plenty of knowledge out there (blogs, courses. conferences, books...) so you'll be able to pick it up much easier than when it was at the embryonic stage and no-one really knew what to use it for. Java is, what, 17 years old now, and people are still starting to learn it now.  No-one said you had to have coded with Java 1.0 in order to be effective in a Java 8 lambdas world.  In fact, you could argue that those who learnt it early on might be less able to adjust to the current state of play.<br /><br />So.  Learn something because it interests you, or it's fun, or you personally can see the value of it. Even the process of learning something new is valuable, even if the thing you learnt is not - it exercises those brain-muscles so they're used to picking up something unfamiliar and playing with it.

> But I see a thousand jobs for Scala/HTML5/&lt;insert tech here&gt;! Should I learn that?

Have you looked at Scala?  Do you like it?  Do you want to learn a whole new language?  Do you want to spend the next two years of your career working in Scala?  Because if you learn it to find a new job, and you <i>do</i> find a new Scala job, then you're going to <i>have</i> to use it, and to continue to learn it. And if you don't really give a crap about Scala, then why bother?  Have you looked at the types of companies that are advertising jobs for Scala?  Do you want to work there?  Again, if not, don't bother.<br /><br />In our industry, particularly if you live and work in places like London, New York, Silicon Valley, there are <i>lots</i> of jobs, even in these Tough Economic Times.  You don't need to take any old job (unless you need a job Right Now, in which case I would advise you take Any Old Job and work on the side to find The Right Job to move to imminently).<br /><br />The point is, you're freaking out because there are all these different technologies and all these jobs that are looking for different combinations of all these different skills, and this is a Good Thing.  You've been looking at it wrong - you think you need to be everything anyone wants, so that someone out there will pick you, like some sort of school sports team selection.  But it's not like that - the selection power is in <i>your</i> hands.  You can wade through those millions of job postings and find the ones that interest you.  You can invest in becoming skilled at the things you like, the things you enjoy, the things that scratch your intellectual itch, and you can then find a job that matches those skills.  Even better, if you're active in learning those skills, and visible at it (stack overflow, your blog, communities...), you're going to <a href="http://java.dzone.com/articles/ghost-who-codes-how-anonymity">improve your chance of getting a job</a> in the area that fascinates you.<br /><br />You don't have to be good at everything.  Just find the things that interest you, stuff you feel motivated to learn about, and then when you find a job that uses those skills, you know you're in the right place.<br /><br />So in fact, there is only one reason to stay ahead of the curve:

1. Because you want to.

So it's much easier to figure out what to spend time learning and what to ignore for now.

You don't have to stay ahead of _all_ the curves.  You just have to stay within tolerance of your own curve.
