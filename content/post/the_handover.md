{
    "disqus_url" : "http://trishagee.github.io/post/",
    "disqus_title" : "The Handover",
    "Title": "The Handover",
    "Pubdate": "2014-06-30",
    "Keywords": ["morphia","releases","process"],
    "Tags": ["morphia","releases","process"],
    "Slug": "the_handover.md",
    "Section": "post"
}

Yesterday I walked into the kitchen to see how lunch was going and my boyfriend handed me a knife, 
a part-chopped hard boiled egg and said "finish this, I need to have a shower". As you do. Apparently there were two things that needed 
doing - "this" needed finishing, and I needed to keep an eye on the fish.

Fine.
<!--more-->

I've "paired" with him while we've made that salad before, and I can tell when a fish is burning.  How hard could it be?

After I finished chopping the egg and putting it into the salad, I realised I didn't know if that was the last thing that needed to go into 
the salad - when he said "finish this", did he mean the whole salad, or just the egg chopping?

(This blog post will be vaguely about technology at some point.  Probably.)

After searching for other eggs that might need to be added, and sifting through the salad to see what was already in there, 
I was still unclear about whether it was "[done](https://www.scrum.org/Resources/Scrum-Glossary/Definition-of-Done)" or not, so I 
went to bother my boyfriend in the bathroom (this is not a euphemism).  

"I told you there were only two things left to do" he said - it was so clear to him what the steps were to finish, 
that he couldn't understand that there might be hidden assumptions in his handover.  All he wanted was for me to finish chopping the 
(only) egg.  Oh and mix it all up. Of course. When I checked if I was supposed to add the olive oil and the salt, the answer was "No, 
I don't trust you to do that" (he's right - I'm English, I didn't even know you could put salt in a salad 
and certainly have no idea about quantities of olive oil. My Spanish boyfriend is genetically wired to know this stuff).

Despite the unclear instructions ("keep an eye on the fish", if taken literally, could result in me watching it burn - fortunately I knew it
was secret code for "remove it from the heat when it's done") we had a very nice lunch.

![Salmon & Salad](/static/images/HandoverSalad.JPG "Salmon and Salad")

There are parallels between this, and what I was struggling with last week (hurrah, we get to the tenuous analogy!).  I've been trying 
to do my first release for [Morphia](https://github.com/mongodb/morphia), the project I'm taking over 
for [MongoDB](http://www.mongodb.org/).  I know my colleague was working hard on an automated release script (one click releasing FTW), 
and I know he invested a reasonable amount of time in automating the release process (this is code for "I had a bad feeling about this").
I was going to be the first to try this out without his machine/settings/user. Yay?

On Friday night Justin gave me some tips of what was involved, finishing with "...and then `.gradlew relase` should just work".  Simples.

Day One: I struggled with the nexus plugin and permissions.

Day Two: I woke up with one of those ideas that hit you in the night and fixed that.

Then I spent two days trying to work out why the Git plugin wouldn't let me log in.

Eventually I realised that for the whole time I hadn't been using the local version of the 
[gradle release plugin](https://github.com/evanchooly/github-release-gradle-plugin) like I thought, 
but an older version. When I fixed that... I spent half a day proving I still had the same issue as before.

Finally, I commented out the code that wasn't working, hard coded a bunch of values and used an old script to upload the Javadoc (don't 
get me started on how long it took me to find how [Maven](http://maven.apache.org/) was populating the release number, 
nor do I want to express the pain I felt at having to install Maven after being in love with [Gradle](http://www.gradle.org/) for the 
last two years).

Eventually [release 0.108 of Morphia](https://github.com/mongodb/morphia/releases/tag/r0.108) went live on Thursday night - huzzah!

But of course, as a responsible human being, rather than high-fiving myself, cracking open a bottle of wine and knocking off for the 
weekend, next I need to prepare the handover for the next person doing the release. Not least because it's probably going to be me, 
and my memory is shocking.  I have two options:

 1. Write a wiki page with the steps needed, manual or automated, including all the local properties that need to be set up as we can't 
 have some of these passwords floating around on GitHub.
 1. Fix the automated release so it really is one click / command

In reality, option 2 still needs documentation because of the local properties that are required.

What I really want to do is crack open that wine.

But the moral of the story is: handovers are hard.  And essential.  And worse, often the person doing the handing over is doing so 
because they're short on time and, for whatever reason, not responsible for the next phase of the project. Combine this lack of time with
all the assumptions and implicit knowledge in that person's head, and the information being transferred is likely to be... less than 
optimal. 

And the handover receiver is now responsible for something they don't have enough knowledge of and they're not even aware of assumptions or 
unknown unknowns. If you're handing over between departments or teams, they might not even have the right tools to find out how to 
progress (Ops teams and testers don't always have access to the code, for example, and if they did might not have the context to find it
useful).

There are tools to help ease the pain of handovers:

 - [Pairing](http://martinfowler.com/bliki/PairProgrammingMisconceptions.html). Pairing might seem expensive (two people at one 
 keyboard?? How will they type fast enough?), but the savings in handover time (and increase in your [Bus Factor](http://en.wikipedia
 .org/wiki/Bus_factor)) make it completely worthwhile.  Pairing with The Boy in making salad meant at least I knew what the steps and 
 ingredients were, I just didn't know what stage we were at. At LMAX, we reduced a lot of our testing backlog by embedding the testers 
 in the development team, and pairing with them at the start and at the end of the [user stories](http://martinfowler.com/bliki/UserStory.html).
 - If you can't do pairing, code reviews help. I was at least aware of our release plugin as I'd seen the original develop in the [Java 
 driver](https://github.com/mongodb/mongo-java-driver/). If I'd been pairing or code reviewing on Morphia, 
 I would have been even more aware of what the steps were and what changes had been made for that project.
 - Finally, if good old fashioned talking isn't your thing, documentation is a good start.  And everyone who uses the docs needs to be 
 able to update the documentation when they find something wrong, missing, confusing, or just want to annotate it with something useful.

For all of these good practices, really what you want is to remove all possible areas of miscommunication. Computers are logical things,
 so if you can write down an exact list of steps that need to be done in order to achieve something, 
you might be able to, I dunno, write that in a script, or something. If you 
<a href="http://www.amazon.com/gp/product/0321601912/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0321601912&linkCode=as2&tag=trissramb-20&linkId=M5DNVR42T66J63VO">Automate All The Things</a><img src="http://ir-na.amazon-adsystem.com/e/ir?t=trissramb-20&l=as2&o=1&a=0321601912" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />, you don't need to have these messy, 
complicated conversations with these messy, complicated people.

But you knew that already.

I'm off to try and fix my script. I've even thought of a way to not need local properties, so maybe next time (or the time after), 
when I have to do a release I'll only have to type a single command. It'll be worth a week or two to implement this if it saves me a week 
like the last one.

But first, that wine...  
  
  
<small>_No boyfriends or colleagues were harmed in the making of this post._</small>