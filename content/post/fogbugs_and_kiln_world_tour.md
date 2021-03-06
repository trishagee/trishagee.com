{
 "disqus_url" : "http://trishagee.github.io/post/fogbugs_and_kiln_world_tour/",
 "disqus_title" : "FogBugs and Kiln World Tour",
 "Title": "FogBugs and Kiln World Tour",
 "Pubdate": "2011-01-18",
 "Keywords": ["tools", "joel", "conferences"],
 "Tags": ["tools", "joel", "conferences"],
 "Slug": "fogbugs_and_kiln_world_tour",
 "Section": "post"
}
Last Thursday I was fortunate enough to get a place on the <a href="http://worldtour.fogcreek.com/">FogBugz and Kiln World Tour</a>. &nbsp;I booked it before I moved jobs, and I'll be honest I had no real interest in the software. &nbsp;I've been reading Joel's books and blogs since my friend Brent bought me <a href="http://www.amazon.co.uk/gp/product/1590593898">Joel on Software</a>&nbsp;and made me read it (he had the foresight to know I'd want to hang on to his copy if he'd lent it to me!). &nbsp;I wanted to see the man in the flesh and hear what he had to say about his software. &nbsp;Because really, do we honestly need yet another bug-tracking / project-management tool?<br /><br /><span class="Apple-style-span" style="font-size: large;">Who would benefit from FogBugz?</span><br /><a href="http://www.joelonsoftware.com/AboutMe.html">Joel</a>'s demo was really good at demonstrating exactly how you might use the software - the processes you might follow, how to raise / update a ticket and chase it, and how you can see what's going on with the projects tracked.<br /><br />I can actually think of a number of companies I've worked for, or friends have worked for, that would see an improvement in productivity from using <a href="http://www.fogcreek.com/FogBugz/">FogBugz</a> for bug tracking / project management. &nbsp;When I worked at Touch Clarity (later swallowed by <a href="http://www.omniture.com/">Omniture</a>, which was gobbled by <a href="http://www.adobe.com/">Adobe</a>) I was desperately looking for a product to help us:<br /><ul><li>Record defects</li><li>Capture new feature requests</li><li>Assign tasks to developers</li><li>Estimate tasks</li><li>Track progress - both at a project level and for individual developers</li><li>Provide us with a lightweight process which was easy to follow</li><li>Generate reports for management.</li></ul><br /><div>From the demo I saw, FogBugz will do everything we wanted at that time. &nbsp;We were using <a href="http://www.bugzilla.org/">Bugzilla</a> back then, and badly. &nbsp;I'd also investigated <a href="http://www.xplanner.org/">XPlanner</a>, <a href="http://www.versionone.com/Product/Product_Planning.asp">VersionOne</a>&nbsp;and a bunch of other defect/project management tools, and not really seen anything that did what I wanted (certainly that was cheap enough). &nbsp;But this was back in 2004/5, we were doing a half-hearted version of <a href="http://www.extremeprogramming.org/">eXtreme Programming</a>, and we didn't have a lot of cash to burn. &nbsp;It was hard then to find a lightweight, customisable, inexpensive tool.</div><div><br /></div><div>The things I saw in FogBugz that I thought would be useful were:</div><div><ul><li>Nice UI - usability of these things is so frequently under-valued.</li><li>Really easy to track what's going on with a defect, to add and edit comments etc. &nbsp;I actually liked that the edit feature still tracked versions of the comments, I can see how some organisations would need that audit trail.</li><li>Evidence-based scheduling - I liked the way that it uses past information to have a good guess at how accurate an estimate will be, and therefore the soonest, likely and latest times a feature might be delivered by.</li><li>Visibility over an individual developer's workload.</li><li>Visibility over work at a project-level</li><li>Loads of charts/reports to let you slice and dice the stuff you have in there.</li><li>Dependency management</li><li>Neat integration to source control - yes, I know you can get this for loads of management tools now, it doesn't mean it's not useful. It seemed pretty slick here.</li><li>It seemed quick. &nbsp;But then it could have been a locally-running instance with about 3 defects in it.</li></ul><br /></div>The things I thought would not be so useful in a more Agile environment:<br /><ul><li>Evidence-based scheduling</li><li>Visibility over an individual developer's workload.</li><li>Lots of the ways the data can be sliced and diced</li><li>Dependency management</li></ul><br /><div><span class="Apple-style-span" style="font-size: large;">So, you like it and you don't like it?</span></div><div>Yeah yeah, I've gone all multiple-personality again. &nbsp;The stuff I liked about the product would be dead useful for the types of projects that work that way - where you assign work to individual developers who estimate the work; where developers are assigned to specific projects; where stories / features might not be broken down into small, independent tasks. &nbsp;These places might be running waterfall, or some agile-ish process, or no process at all. &nbsp;A tool like this will give them much better visibility over what's going on, over which deadlines won't be met, over who's estimates are flaky and who's are generally reliable.<br /><br /></div><div>However even before I joined <a href="http://www.thoughtworks.com/">ThoughtWorks</a>, before I joined <a href="http://www.lmaxtrader.co.uk/about-lmax">LMAX</a>, I was sold on Agile as a more natural way to run development teams (this is despite having worked with Touch Clarity's sort-of-XP and A Very Large Media Organisation's <a href="http://bitsnwidgets.com/2008/04/19/DontBeASCRUMBUT.aspx">ScrumBut</a>). &nbsp;The problems that some of the features in FogBugz tries to address are similar to the problems that Agile (<a href="http://www.extremeprogramming.org/rules.html">XP</a>/<a href="http://www.scrumalliance.org/learn_about_scrum">Scrum</a>/<a href="http://availagility.co.uk/2008/10/28/kanban-flow-and-cadence/">Kanban</a> or some hybrid of these) is also supposed to address.</div><div><ul><li>Evidence-based scheduling: I totally agree with getting statistical about this - teams and management should have a good idea how reliable estimates are. &nbsp;But one of the ways to reduce the variation is to have the estimates done by the team. &nbsp;At LMAX, we would have three developers estimate every story. &nbsp;With any luck at least one of those would know enough about it to provide some solid technical guidance on what was involved, but if there wasn't someone in a group of three that had that knowledge, chances were pretty good the team generally were going to be pretty vague on it. &nbsp;Granted, if you're using FogBugz you can enter the team estimate instead of just the individual who is going to implement it and then your evidence-based scheduling will be for team-estimates instead of personal ones. &nbsp;This is totally fine, in fact it's a good thing - I just think we shouldn't use evidence-based scheduling to "fix" the problem that estimates are just that - an estimate, a guess.</li><li>Visibility over a developer's workload: If you're doing pair programming (XP), if the team takes ownership of the implementation of features / stories (Scrum), there's no need to look at how busy an individual developer is. &nbsp;Yes, there are lots of organisations that do allocate work to individuals. &nbsp;In many (most?) Agile-practicing teams, this will not be happening. &nbsp;So really you only need visibility over a team or project level.</li><li>Reporting: Ah, I love reporting. &nbsp;I love data, statistics, pretty charts. Maybe I'm secretly a project manager. &nbsp;But it's SO easy to get hung up on the stats, on one tiny measurement, rather than the bigger picture - are we getting closer to "done" or not? &nbsp;I think you should be able to get at all that data, but not get carried away micro-optimising for metrics which may be hiding bigger problems.</li><li>Dependency management: another thing that is dead important in some types of teams or organisations. &nbsp;But the last few Agile projects I've worked on have not tracked hard-link dependencies at all - each story should stand alone, should be estimated on the basis of just doing that piece of work. &nbsp;Yes, this is idealistic, and even in the projects where we did not officially track dependencies, we'd have a good idea of a very general order things should be done in (or an idea of the order things could be done in to make life easier). &nbsp;But these things can be fluid, if a specific feature needs to be done now, you shouldn't have to do every single story that might have a tiny piece of functionality this story is dependent on - just tackle this story and everything you need for it. &nbsp;</li></ul><div>All of those points could be blog posts in their own right, I know it's taken me years to get my head around the way I personally see Agile. &nbsp;But you get the idea, or maybe you don't - that's fine, maybe you're in exactly the sort of place that could use FogBugz to improve your productivity.</div></div><div><br /></div><div><span class="Apple-style-span" style="font-size: large;">FogBugz vs Mingle</span></div><div>I started at <a href="http://www.thoughtworks.com/">ThoughtWorks</a> last week, so I'd better mention that <a href="http://www.thoughtworks-studios.com/">ThoughtWorks Studios</a> have a competitor product, <a href="http://www.thoughtworks-studios.com/mingle-agile-project-management">Mingle</a>. &nbsp;I'm reasonably well-qualified to talk about it since I've been using it in anger for the last two years in a maturing agile environment, and&nbsp;I had my Mingle&nbsp;<s>indoctrination</s>&nbsp;induction last week.</div><div><br /></div><div>To me, the main difference is the angle the two products are taking to approach the same problem: how do you provide a tool that</div><div><ol><li>is easy and lightweight enough to use that people (particularly developers) will keep it up to date;</li><li>tracks just the right amount of data that people have visibility over the state of development (What are we doing? &nbsp;Are we going to hit our deadlines? What are our blockers?)</li></ol><br /><div>To me, it seems FogBugz is coming from the traditional development model - it might not be anything as formal as waterfall, but it may not be based on short iterations and assumes individuals rather than teams are assigned work. &nbsp;Mingle was developed for the Agile team, e.g. collective responsibility, pair programming, short iterations.</div></div><div><br /></div><div>Mingle is highly configurable, and while FogBugz has a number of templates and custom work flows, Mr Spolsky specifically stated at the demo that these really shouldn't be used. &nbsp;That they've worked hard to find a process that works, and we should all follow that.</div><div><br /></div><div>So, Mingle embraces the differences between teams/processes and FogBugz specifically discourages it.</div><div><br /></div><div>I reckon these things are actually also the potential downfalls for both products too: &nbsp;Mingle can be abused so badly that it adds no value; FogBugz could be so prescriptive it slows down productivity.</div><div><br /></div><div>But it's horses for courses, every tool has its advantages and disadvantages. &nbsp;Or should I be pushing Mingle at this point until I pass my probation??</div><div><br /></div><div><span class="Apple-style-span" style="font-size: large;">Kiln, and an introduction to DVCS</span></div><div>Good Lord, I've written all that stuff and that's only from the short demo at the start of the day.</div><div><br /></div><div>Fortunately I have a lot less to say about the latter part. &nbsp;It was an introduction to Distributed Version Control (DVCS), and it was pitched absolutely right for someone like me. &nbsp;</div><div><br /></div><div>I've never used a DVCS; most recently I've been using <a href="http://subversion.tigris.org/">Subversion</a>, but I've also used <a href="http://pvcs.synergex.com/">PVCS</a>, <a href="http://www-01.ibm.com/software/awdtools/clearcase/">ClearCase</a>, <a href="http://msdn.microsoft.com/en-us/library/aa302175.aspx#vssmap_topic2">VSS</a>&nbsp;and a bunch of others (in fact, I'm pretty sure I've had to learn a new source control system every time I've switched project or company!). &nbsp;I've been introduced to <a href="http://git-scm.com/">Git</a>&nbsp;over a lunchtime, and I read Martin Fowler's blog post on <a href="http://martinfowler.com/bliki/VersionControlTools.html">version control tools</a>. &nbsp;The intro provided by FogCreek was spot on for me. &nbsp;It showed me:</div><div><ul><li>The differences between a DVCS and something like Subversion (OK, specifically svn, which is fine for me);</li><li>Advantages of using a distributed source control system;</li><li>Some mindsets that you need to change when switching from svn to a DVCS like <a href="http://mercurial.selenic.com/">Mercurial</a>;</li><li>The FogCreek way of setting up the repositories.</li></ul><br /><div>The last point was particularly useful in giving some real-life examples of how to use a DVCS and why.</div></div><div><br /></div><div>Then there was some stuff on why <a href="http://www.fogcreek.com/kiln/">Kiln</a> might give you more than just the freebie Mercurial install.</div><div><br /></div><div>It was more useful in a general fashion than the FogBugz section. &nbsp;However, like the FogBugz talk, I got a good feel for the types of teams/companies Kiln might be good for, and why you might use it. &nbsp;Personally it convinced me that using a DVCS in general is probably better than Subversion (insert usual disclaimer of different tools being appropriate for different situations). &nbsp;It certainly encourages working practices that will lead to a) less accidental loss of code (after all, that's what source control is for) and b) if well organised, better separation of bugs / features / stories and better integration across versions and branches.</div><div><br /></div><div>If you want to know what I've been blathering on about in this section, check out Joel's <a href="http://hginit.com/00.html">excellent introduction to Mercurial</a>. &nbsp;OK, I admit it, I haven't read it all. &nbsp;But it seems to cover everything that was covered in the conference session, with Joel's usual wit and appeal to the developer mindset.</div><div><br /></div><div><span class="Apple-style-span" style="font-size: large;">In Other News</span></div><div>In terms of an education session, the "World Tour" was excellent - succinct, easy to digest, and (to my mind) aimed exactly at the audience.</div><div><br /></div><div><i>However</i>. &nbsp;I actually ended the (half) day being slightly disappointed, and not just because these tools don't seem to be ideal for the Agile team.&nbsp;</div><div><ul><li>I didn't get enough of a chance to network. &nbsp;Now, I'm happy to admit this is a problem I regularly have - because, like many developers, I find it difficult to talk to new people in a big room full of people I don't know. &nbsp;However, given that this was a big room full of developers, I wish there had been more of an effort made to help us to mix and network. Before the talks we were on tables in another room having coffee etc, which I liked because it did lead to some conversation in small groups. &nbsp;But I would have been nice if there had been a chance at the end of the talks to chat to people and&nbsp;dissect&nbsp;the session (if there actually was, it was so badly publicised I missed it). &nbsp;I went with a stack of business cards and didn't give a single one out.</li><li>The half day didn't seem like enough. &nbsp;But this might be more a reflection of the above point since I got what I wanted from the talks, any more would have been too much info. &nbsp;So maybe I just wanted more time with the attendees and with the FogCreek guys.</li><li>I was shocked by how few women there were. &nbsp;I'm no tech newbie, I've been to training sessions, conferences, user groups, seminars, and worked on site at a lot of different types of places. &nbsp;I was very surprised to see that in a room of several hundred people I counted 5 women (myself included). &nbsp;This seems low even for gathering of techies, it seems <i>very</i> low for a presentation on a piece of software that is effectively project management software. &nbsp;I don't have the stats to hand, but in my personal experience any technical event with even a sniff of project management stuff is better represented across both genders. &nbsp;I wouldn't normally comment on it because it's something I'm used to myself, but I've been asked a bunch of times in the last two weeks "what do we need to do to encourage more participation by women?", and I have my eyes open for stuff which might help me answer that.</li></ul><br /><div><span class="Apple-style-span" style="font-size: large;">In Conclusion</span></div></div><div><ol><li>A generally good, well-run event, especially as it was free (if I recall correctly).</li><li><a href="http://www.fogcreek.com/fogbugz/">FogBugz</a> and <a href="http://www.fogcreek.com/kiln/">Kiln</a> are excellent tools for a certain type of organisation / team, and I'm not talking about a small minority of teams here.</li><li>If you're Agile, these tools are probably not for you. &nbsp;You can get them to work, and if you're "kind of" agile they're probably better than a lot of your options. &nbsp;But true agile teams running an effective process might find themselves hindered more than helped.</li><li>I'm going to download and install a DVCS the very next time I have to write a line of code.</li></ol><br /><br /></div>
