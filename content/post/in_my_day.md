{
 "disqus_url" : "http://trishagee.github.io/post/in_my_day/",
 "disqus_title" : "In my day...",
 "Title": "In my day...",
 "Pubdate": "2014-03-03",
 "Slug": "in_my_day",
 "Section": "post"
}
<div style="float: left; margin-right: 10px;"><script type="text/javascript">var dzone_url = 'http://java.dzone.com/articles/my-day';</script><script type="text/javascript">var dzone_title = 'In my day...';</script><script type="text/javascript">var dzone_blurb = '[description]';</script><script type="text/javascript">var dzone_style = '1';</script><script language="javascript" src="http://widgets.dzone.com/links/widgets/zoneit.js"></script></div> Web development has changed a <i>lot</i>.<br /><div class="p2"><br /></div><div class="p1">I was aware that there have been many changes in the last few years, and I’ve seen maturity come to web platforms in the form of standardisation and common reusable libraries and frameworks - and I don’t mean reusable in the way we used to “reuse” stuff by nicking it off other people’s websites when we saw something cool.</div><div class="p2"><br /></div><div class="p1">I used to be a web developer. &nbsp;Sort of. &nbsp;Some times I’ve been on the bleeding edge, and others… I remember using JavaScript to call back-end services with an XML payload before people were using the term AJAX, but I also remember working on an enterprise um… “classic”… JSP application only “recently” - in fact that was probably the last job where I did anything that looked like web development.</div><div class="p2"><br /></div><div class="p1">So this blog post is going to chart the progress of web development through my own experience.&nbsp; Of course, this doesn’t by any means cover the whole spectrum, but I think my experience has been not unusual for a Java programming working through the noughties.</div><div class="p2"><br /></div><div class="p1">Over the course of my career I moved further away from the UI, because certainly early on the money and status was in “back end”, whatever that means, and not “front end”. &nbsp;Which is ridiculous, really, especially as back then you couldn’t really follow best practices and clean code and test first and all that awesome stuff when doing front end development because none of the browsers played by the rules and frankly if you got it working at all you were a bloody genius. &nbsp;And that’s not even considering the fact that as a “front end” developer you should be thinking about actual real human beings who use your product, and actual real human beings are messy things and understanding them is not (we’re told) traditionally a domain that we developers are naturally proficient in.</div><div class="p2"><br /></div><div class="p1">Anyway, I digress. &nbsp;This was supposed to be a history lesson. &nbsp;Or a nostalgia trip. &nbsp;Or possibly Ranty Trish waving her walking stick in the air and shouting “You kids don’t know how good you’ve got it these days”. &nbsp;If nothing else, I hope that it makes other “back end” developers like myself appreciate how much things have moved on.</div><div class="p2"><br /></div><div class="p1">Let’s go back to the olden days, before I’d even graduated: picture a time before smart phones - before phones were even common (I was horribly mocked at university for being poncy enough to have a mobile), before we knew if all this work we were doing to combat the millennium bug was going to stop the end of the world. &nbsp;I was doing my first summer internship at <a href="http://corporate.ford.com/">Ford</a>, and a contractor from Logica (who don't seem to exist any more??) told me that if I was messing around with web pages and HTML (my friends and I had geocities-and-equivalent sites) I should look at this JavaScript thing to make my pages “dynamic”. &nbsp;I didn’t have to just use GIFs to bring my page to life, I could move stuff around on the page. &nbsp;I think I wrote a “you are in a crowded room”-type adventure game, because my background was BASIC and that’s what you do.</div><div class="p2"><br /></div><div class="p1">Actually I haven’t even mentioned that we were creating these websites to stay in touch with each other. &nbsp;We’d discovered guest books, and used them to write comments and share stories since we’d all moved out of our home town to go to different universities. &nbsp;Man, why didn’t I invent Facebook back then? &nbsp;That’s what we needed.</div><div class="p2"><br /></div><div class="p1">Anyway.</div><div class="p2"><br /></div><div class="p1">A year later, I was back at Ford doing my <a href="http://en.wikipedia.org/wiki/Sandwich_degree">sandwich year-in-industry</a>. &nbsp;The first project I worked during this time was a web-based reporting tool that needed to dynamically display hierarchical data. &nbsp;We chose JavaScript trees to render this data - my year of messing around with my website paid off, and I was able to use my “cutting edge” Javascript skills in a real production environment. &nbsp;Yay? &nbsp;The back end was CGI - I think I was writing in Perl, but don’t tell anyone that. &nbsp;I was learning Java at university, but this was a new language and I don’t think Ford was using it yet.</div><div class="p2"><br /></div><div class="p1">The next project was a very ambitious one - be the first car manufacturer to <a href="http://www.brandrepublic.com/news/11990/Ford-Vauxhall-cut-online-car-prices/?HAYILC=RELATED">sell new cars on the web</a>. &nbsp;Ford was well ahead of their time - the millennium bug had not killed us all, but people were barely buying books online, never mind spending tens of thousands of pounds on a car they’d never driven. &nbsp;But it wasn’t just ahead of its time from a business point of view, technically it was very advanced too - we used lots of “DHTML” (as we were now calling it), a new-fangled technology called ASP, and we were writing modular, reusable <a href="http://www.microsoft.com/com/default.mspx">COM</a>ponents. &nbsp;We used XSLT to parse the XML from the COM objects, and the ASP figured out whether you were Netscape or Internet Explorer (Firefox wasn’t even a gleam in the inventor’s eye, and forget Chrome, I think we using <a href="http://www.altavista.com/">Alta Vista</a> (whaaaat? AltaVista got bought by Yahoo??) not some new-fangled search engine beginning with G) so it could use the right XSLT to turn the XML into HTML that was readable by the browser you were using. &nbsp;My job was to get the DHTML pages rendering and animating correctly in both IE4 and Netscape 4. &nbsp;That was a lot of fun for me, but also very challenging.&nbsp; And imagine my shock when a few months later I tested the site from the university UNIX machines to find that Netscape rendered it completely differently under UNIX.&nbsp; I learnt a lesson about how important it was to test on different platforms.</div><div class="p2"><br /></div><div class="p1">We had some smart Microsoft people helping us out with this project, and, because it was 2000 and the <a href="http://en.wikipedia.org/wiki/Dot-com_bubble">dot com crash</a>&nbsp;hadn’t happened just yet, we also had a lot of young, overpaid, overconfident contractors who believed anything was possible. &nbsp;I learnt a lot during this time, not just about the technology, but also about different approaches to shaping your IT career. &nbsp;And about how much you could earn before you were 25. &nbsp;I was definitely going to be a programmer when I left university the next year.</div><div class="p2"><br /></div><div class="p1">Yeah, so… I graduated in 2001. &nbsp;If you were around then, you’ll remember that getting a job was a bit more difficult than I had anticipated, especially as these young, overpaid contractors were now desperately grabbing anything they could find. &nbsp;But that’s a story for another day.</div><div class="p2"><br /></div><div class="p1">I didn’t go back to Ford straight away, I’d “been there and done that”. &nbsp;I worked on the website for <a href="http://commonpurpose.org.uk/">Common Purpose</a>. &nbsp;On the first day, they sat me down with <a href="http://www.amazon.com/gp/product/1861003625/ref=as_li_tf_tl?ie=UTF8&amp;camp=1789&amp;creative=9325&amp;creativeASIN=1861003625&amp;linkCode=as2&amp;tag=trissramb-20">a book on JSP and Servlets</a>, and that was my reading material for the next few weeks. &nbsp;If I’d been fresh out of university where we’d been doing Applets, and where I’d written a Swing app on the side for my Dad’s school, this would have been a big mindset change for me. &nbsp;But having worked on the ASPs it wasn’t such a big shift. &nbsp;I did, however, like how JSPs and servlets made the separation between the view and all-of-the-other-logic-stuff a bit clearer - back in ASP-land we’d settled on a convention of dealing with the form data from the previous page in the first part of the ASP, and rendering the new page in the second part. &nbsp;To this day I still don’t know what we should have been doing instead. &nbsp;But in JSP-land it only took me... I dunno, about 6 months I think, to get the website up and running. &nbsp;The most difficult section was <a href="http://web.archive.org/web/20021001132257/http://www.commonpurpose.org.uk/home/apply-online.vdf">registrations</a>. &nbsp;And yes, I was a graduate, and yes, I was new, but that was a good turnaround for a web application “in those days”.</div><div class="p2"><br /></div><div class="p1">In my spare time I used what I’d learnt on <a href="http://blews-ltb.co.uk/knot.asp">the blews website</a>. &nbsp;I even had a section where people could log in and <a href="http://web.archive.org/web/20050322033948/http://www.blews-ltb.co.uk/photographs/photo.jsp?section=20">comment on photos</a>&nbsp;- we had whole conversations on this website. &nbsp;It was a way for me and my friends to stay in touch. &nbsp;If I’d cracked the photo-uploading instead of it being a manual process for me, I would have invented Facebook. &nbsp;If only I’d known….</div><div class="p2"><br /></div><div class="p1">The work dried up and there was nothing else for a graduate in the early noughties, so I went back to Ford. &nbsp;My first role back I picked the same technologies we’d been using before - XML, XSLT, only this time we were using JSPs instead of ASP. &nbsp;Our project had a very tight budget and we’d worked out that using open source Java technologies and running the application on one of the many UNIX machines lying around the place was a lot cheaper than the Microsoft solution. &nbsp;I think we were the first team in Ford Europe to pick Java at a time when the recommended approach was Microsoft. &nbsp;We delivered on time and under budget, and Java was the way forward for the department from then on. &nbsp;But on this project I met a guy who would impact my career probably more than he even realises, a guy I’d work with again later. &nbsp;He told me that in Java we no longer used Vector by default, but ArrayList (whaaat? What’s an <a href="http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html">ArrayList</a>? I had no idea what the differences were between Java 1.1, which we’d learnt at university, and Java 1.2, which was now standard). &nbsp;And questioned my choice of XML/XSL. &nbsp;Although I’d been learning new technologies and growing, he was the one who made it clear to me that I needed to keep myself ahead of the curve with the technologies I was using, or planned to use, if I wanted to stay relevant and make my life easier.</div><div class="p2"><br /></div><div class="p1">On the next project I worked with a genius guy who was definitely keeping ahead of the curve - he was using JavaScript to send small XML payloads to the server (which was coded in Java), and rendering the response in place on the page instead of reloading the whole thing. &nbsp;Mind. &nbsp;Blown. &nbsp;I didn’t even hear the term <a href="http://en.wikipedia.org/wiki/Ajax_(programming)">Ajax</a>&nbsp;until a year or more later. &nbsp;We were fortunate in that this was once again an internal application, so we controlled the browser. &nbsp;This was back in the days when you wanted your users to be on IE5, as this was the only browser that supported this functionality.</div><div class="p2"><br /></div><div class="p1">The next few projects/jobs I worked on were all more pedestrian variations on the JSP theme - first I learnt <a href="https://struts.apache.org/release/1.3.x/userGuide/release-notes-1_1.html">Struts</a>, which at least made us realise there was a model, a view, and a controller. &nbsp;Then at <a href="http://web.archive.org/web/20050211061038/http://www.touchclarity.co.uk/">Touch Clarity</a> I learnt about <a href="https://spring.io/blog/2004/03/24/spring-framework-1-0-final-released">Spring MVC</a>, which actually put the validation errors next to the boxes which cause the error - by default, without you having to mess around. &nbsp;Spring was a revelation too, a framework that really tried not to get in your way. &nbsp;It was also frustrating because you needed to understand its lifecycle, but it did so much heavy lifting for you, it sped up standard CRUD-app web development enormously.</div><div class="p2"><br /></div><div class="p1">A couple of years passed, during which time I was still working on a web application (for an investment bank) but I can’t for the life of me remember what technologies we used (other than Java). &nbsp;I know it was hard to test and I know the tricky stuff was “back end” not “front end”.</div><div class="p2"><br /></div><div class="p1">In the next project where I had any control of the technology, I picked Spring since I’d had such a good experience previously. &nbsp;It took 4 developers a couple of months or so to develop an admin application for a trading app. &nbsp;Given the previous timescales I’d worked with, this seemed pretty good. &nbsp;Until a few months later and two other guys on the project produced an admin app for our bank users in a matter of weeks. &nbsp;I can’t remember what they used, maybe <a href="http://grails.org/">Grails</a>? &nbsp;But it was another demonstration of how I really should have been researching the field instead of simply sticking with what I knew, especially when I knew my knowledge was a couple of years out of date.</div><div class="p2"><br /></div><div class="p1">Fast forward to <a href="http://www.lmax.com/">LMAX</a>, and we were using <a href="http://en.wikipedia.org/wiki/Google_Web_Toolkit">GWT</a>, pre-2.0 - I think this probably feels natural if you’ve been a Swing or AWT developer, but I’m still not convinced it’s a sound web platform (although I know it has improved). &nbsp;It was great because cross-browser was no longer an issue, but it was bad because it separates you from the underlying HTML, which means you can <a href="http://mechanitis.blogspot.co.uk/2011/01/gwt-why-verticalpanel-is-evil.html">seriously mess up without realising</a>. &nbsp;It’s also hard to use CSS correctly when you don’t have access to all the HTML components.</div><div class="p2"><br /></div><div class="p1">So we come to more-or-less the present day, as it should be fairly obvious that during the time I’ve been working on the <a href="https://github.com/mongodb/mongo-java-driver">MongoDB Java Driver</a>&nbsp;I haven’t done a lot of GUI development. I’m lucky because attending lots of conferences means I see a lot more of the current-trending technologies, but up until a couple of weeks ago I hadn’t had a chance to play with any of them.</div><div class="p2"><br /></div><div class="p1">So now I’ve been trying <a href="http://angular.js/">Angular.js</a>, <a href="http://getbootstrap.com/">Bootstrap</a>, and <a href="http://angular-ui.github.io/bootstrap/">UI Bootstrap</a>. &nbsp;My goodness. &nbsp;It’s a whole 'nother world. &nbsp;I’m seeing at conferences and user groups that developers are increasingly polyglot, so maybe there’s no such thing as “just” a Java developer any more, but if you are “just” a Java developer, I think it could be… interesting… to get your head around some of the techniques. &nbsp;Since we don’t have closures, our callbacks are ugly and we tend not to program that way. &nbsp;Async is not something that comes naturally in a Java environment, I believe, although after working that way at LMAX I’m personally sold on it. &nbsp;Old-world JavaScript developers like I am/was might also find it hard to understand you can have clean, testable JavaScript code which Just Works. &nbsp;It didn’t even occur to me to worry about browser compatibility, and my app not only worked on my phone as well as my laptop, but looked really phone-ish and awesome with very minimal effort.</div><div class="p2"><br /></div><div class="p1">I’m currently on a plane on the way to QCon London where I’m <a href="http://qconlondon.com/london-2014/presentation/HTML5,%20Angular.js,%20Groovy,%20Java,%20MongoDB%20all%20together%20-%20what%20could%20possibly%20go%20wrong?">going to demo</a> this Brave New World of web development (together with a nice Java back end to prove how awesome Java is to work with and, of course, a MongoDB database). &nbsp;So it is not my intention in this post to explore what this new world looks like. &nbsp;But I have seen the Present, and it’s a lot better than the Past. &nbsp;Kids These Days don’t know how good they’ve got it - they’ve never had to struggle, to fight the browser, to hand-craft their JavaScript like we have, or had to work with raw, low-level JSPs and Servlets.</div><div class="p2"><br /></div><div class="p1">Now things are easier. &nbsp;There are standards, there are libraries, there are best practices and YouTube videos showing you <a href="http://www.youtube.com/watch?v=i9MHigUZKEM">how to create apps in 60 minutes</a>&nbsp;(back in My Day I had to borrow someone else’s browser to use the Internet, and I debated for years the value of spending my own actual money on a Javascript actual paper actual book, which I could not afford). &nbsp;Now, you can get something quite pretty and functionally interesting, working in a lot less time than I realised. &nbsp;But that doesn’t mean the Kids These Days have it easier - it means there is so much more potential. &nbsp;Instead of beating your head against trying to get a specific version of IE to do what you want, instead of having to write separate pages for different browsers (although maybe that still goes on), you can be exploring so much further into the possible, try things that no-one else has done yet. &nbsp;It opens up so many interesting possibilities for apps on all platforms.</div><div class="p2"><br /></div><div class="p1">Exciting times.</div><div class="p2"><br /></div><br /><div class="p1">So next time someone asks me “What is the de facto front-end framework for Java?” I’m going to say HTML5, CSS and JavaScript.</div>