{
 "disqus_url" : "http://trishagee.github.io/post/my_summary_of_geecon_krakow/",
 "disqus_title" : "My Summary of GeeCON, Krakow",
 "Title": "My Summary of GeeCON, Krakow",
 "Pubdate": "2013-05-22",
 "Keywords": ["conferences", "video"],
 "Tags": ["conferences", "video"],
 "Slug": "my_summary_of_geecon_krakow",
 "Section": "post"
}
Last week I was in Krakow, Poland for <a href="http://2013.geecon.org/">GeeCON</a>. &nbsp;Which was excellent! &nbsp;I find it really
interesting that conferences all have their own personalities, that they are not all the same.
<div class="separator" style="clear: both; text-align: center;"><a href="http://2.bp.blogspot.com/-QGi20Kv1QL0/UZyWDc9hzVI/AAAAAAAALj0/ZlJ-1o1rLBk/s1600/2013-05-18+19.35.58.jpg" imageanchor="1" style="clear: right; float: right; margin-bottom: 1em; margin-left: 1em;"><img border="0" height="320" src="http://2.bp.blogspot.com/-QGi20Kv1QL0/UZyWDc9hzVI/AAAAAAAALj0/ZlJ-1o1rLBk/s320/2013-05-18+19.35.58.jpg" width="240" /></a></div>
GeeCON had its own distinct personality. &nbsp;If you're a Java/JVM person based in Poland, I would highly recommend it - more than 90%
of the attendees were Polish (probably the remainder were largely speakers) so this conference is very much for you. &nbsp;The quality
of the speakers was really good too, I learnt a lot off many of them.

From a speaker's point of view, there were some cultural things which took a bit of getting used to. One of the good things was that the
audience was very keen on asking questions, they were much more interactive than a typical London audience (for example). However,
I'm accustomed to quite short questions, and I found that the audience liked to give a lot of detail in their questions and frequently
ask more than one at once - this meant that all the speakers really needed to allocate a lot more time for Q & A than expected. One
of the other things I found unusual was the number of people who would walk in and out of the room during sessions - this wasn't just
everyone fleeing my session (I hope!), I saw it happen in all the talks, even the keynotes.

## My stuff
On the first day I was on a panel about diversity in IT, which was basically about women programmers (again). It was a good panel to be
on, actually, because there were a range of opinions, including downright disagreement, which made for a more interesting discussion.
Sadly it left the audience with too little time to contribute though.

On the second day I was presenting ["What do you mean, backwards compatibility?"](http://vimeo.com/72982916),
which elicited a lot of responses from the audience. &nbsp;I think I got the balance right between providing food for thought for any
Java programmer, and enough of a look into what we're considering for the new MongoDB Java driver,
that it felt like I satisfied the two audiences - those who are interested in MongoDB with Java,
and those who... aren't (yet).

But it wasn't my experience as a speaker which really made GeeCON for me. &nbsp;For the first time in ages I felt like I learnt
something as an attendee. &nbsp;I don't know if that's because a) I only had one presentation to prepare so I had time for a lot of
sessions b) we have some specific problems we're trying to solve on our code right now that we're looking for answers to or c) the
conference inspired it, but I came out of a lot of sessions excited about things to try.

## Testing
My first take-away point is to try <a href="https://code.google.com/p/spock/">Spock</a>. I've been told for ages that I need to give it a
 go, but the session really sold it to me. &nbsp;It seems to have features that will solve specific things we're looking at right now,
 including:

- Simplifying mocking
- Annotating tests with properties (e.g. `@Slow`)
- Running the same test with different sets of data, instead of having to copy-paste the test a bunch of times
- Reporting of failures, particularly power assert and `@Unroll`, make diagnosing failures much simpler.
- Using BDD terms as keywords (given/when/then) means the tests really do document themselves.

I'm totally sold on it. &nbsp;I was concerned, because we're writing an open source Java library and I want the unit/integration tests
to be understandable to Java developers, and I worried that adding Groovy tests might make the learning curve steeper. &nbsp;But I think
it's an idea worth playing with.

## Asynchronous IO
So one of the things we're working on is trying to figure out the best way to provide an async Java driver. <a href="http://2013.geecon
.org/speakers/erik-onnen">Erik Onnen</a>'s talk around performance network programming on the JVM was really interesting. &nbsp;Most
usefully, it compared sync to async communication, outlining the pros and cons, and how you can do it on the JVM.

## Build the right thing before you build the thing right
The first keynote was about [Pretotyping](http://www.pretotyping.org/) - Patrick Copeland from Google was talking
about ideas and innovators, and blowing away the myth that all it takes to make money is a single great idea. He highlighted how
really great ideas aren't necessarily successes, and some ideas that sound great don't feel right in practice. Pretotyping is a
way to test things like:

<a href="http://3.bp.blogspot.com/-pgXRSN4oq0k/UZyVTqpUoFI/AAAAAAAALjk/1evlD4F4nYY/s1600/2013-05-15+10.30.13.jpg" imageanchor="1" style="clear: right; float: right;
margin-bottom: 1em; margin-left: 1em;"><img border="0" height="240" src="http://3.bp.blogspot.com/-pgXRSN4oq0k/UZyVTqpUoFI/AAAAAAAALjk/1evlD4F4nYY/s320/2013-05-15+10.30.13.jpg" width="320"></img></a>
<ul><li>Would you use it / do it?</li><li>How would you interact with it?</li><li>Is it socially acceptable to use it in the
circumstances?</li></ul>

Because it's very low tech, very low effort (think post-its and note pads, not HTML prototypes) it facilitates fast failure (therefore
reducing the cost).

The session was videoed, so hopefully it will be available to see. If you're thinking of An Idea, I highly recommend this talk.


## Many users = anthropology, not user experience
<a href="http://www.joelonsoftware.com/">Joel Spolksy</a>, the man who inspired me to start this very blog (well,
earlier incarnations of it) talked about the experiences of growing stack exchange. This was interesting because it was not about
the technology, but about subtle things you can do to influence user's behaviour - for example, reputation rewards "good" behaviour,
and a better reputation means you are trusted to do more on the site.

This was another inspiring talk if you're interested in creating a product or company.

<div class="separator" style="clear: both; text-align: center;"><a href="http://4.bp.blogspot.com/-P-ejmRc3bsg/UZyUtEyArWI/AAAAAAAALjc/qP2tXp-nZkY/s1600/2013-05-18+20.09.07.jpg" imageanchor="1" style="margin-left: 1em;
margin-right: 1em;"><img border="0" height="300" src="http://4.bp.blogspot.com/-P-ejmRc3bsg/UZyUtEyArWI/AAAAAAAALjc/qP2tXp-nZkY/s400/2013-05-18+20.09.07.jpg" width="400" /></a></div>

As always, I also met a lot of really interesting people who gave me a lot to think about. I've come back more motivated than ever to work on my various projects.

So, Krakow is beautiful, and GeeCON is a good learning experience. &nbsp;Go next year if you can!
