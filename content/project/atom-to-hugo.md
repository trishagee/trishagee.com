{
    "disqus_url" : "http://trishagee.github.io/post/atom-to-hugo",
    "disqus_title" : "Converting Blogger to Markdown",
    "Title": "Converting Blogger to Markdown",
    "Description": "Adventures in trying out Hugo for creating my blog content",
    "Pubdate": "2014-03-20",
    "Keywords": ["code", "groovy", "hugo", "github", "intellij"],
    "Tags": ["code", "groovy", "projects"],
    "Slug": "atom-to-hugo",
    "Section": "project"
}

I've been using [Blogger](http://www.blogger.com/) happily for three years or so, since I migrated the blog from [LiveJournal](http://www.livejournal.com/) and
decided to actually invest some
time writing.  I'm happy with it because I just type stuff into Blogger and It Just Works.  I'm happy because I can use my Google
credentials to sign in.  I'm happy because now I can pretend my two [Google+](https://plus.google.com/+TrishaGee/) accounts exist for a purpose,
by getting Blogger to automatically share my content there.

A couple of things have been problematic for the whole time I've been using it though:

1. Code looks like crap, no matter what you do.
2. Pictures are awkwardly jammed in to the prose like a geek mingling at a Marketing event.

The first problem I've tried to solve a number of ways, with custom CSS at a blog- and a post- level.  I was super happy when I
discovered [gist](http://gist.github.com), it gave me lovely content highlighting without all the nasty CSS.  It's still not ideal in a
blogger world though,
as the gist doesn't appear in your WYSIWYG editor, leading you to all sorts of tricks to try not to accidentally delete it. Also I was
too lazy to migrate old code over, so now my blog is a mish-mash of code styles, particular where I changed global CSS mulitple times,
leaving old code in a big fat mess.  There's a lesson to be learned there somewhere.

The second problem, photos, I just gave up on. I decided I would end up wasting too much time trying to make the thing look pretty,
and I'd never get around to posting anything.  So my photos are always dropped randomly into the blogs - it's better than a whole wall of
prose (probably).

But I've been happy overall, the main reason being I don't have to maintain anything, I don't have to worry about my web server going
down, I don't have versions of a blog platform to maintain, patch, upgrade; I can Just Write.

But last week [my boss](http://spf13.com) and [my colleague](http://christiankvalheim.com/)  were both on at me to try [Hugo](http://spf13.com/project/hugo),
a site generator created by my boss.  I was resistent because I do not want to maintain my own blog platform,
but then Christian explained how I can write my posts in [markdown](http://daringfireball.net/projects/markdown/), use Hugo to generate the content,
and then host it [github pages](http://pages.github.com/). It sounded relatively painless.

I've been considering a move to something that supports markdown for a while, for the following reasons:

1. These days I write at least half of my posts on the plane, so I use TextEdit to write the content,
and later paste this into blogger and add formatting.  It would be better if I could write markdown to begin with.
2. Although I've always disliked wiki-type syntax for documentation, markdown is actually not despicable,
and lets me add simple formatting easily without getting in my way or breaking my flow.

So I spent a few days playing with [Hugo](http://hugo.spf13.com/) to see what it was, how it worked, and whether it was going to help me.  I've come up with a
few observations:

**Hugo really is lightning fast**.  If I add a `.md` file in the appropriate place, and with the Hugo server running on my local machine
it will turn this into real HTML in (almost) less time than it takes for me to refresh the browser on the second monitor.  Edits to existing
 files appear almost instantly, so I can write a post and preview it really easily.  It beats the hell out of blogger's Preview feature,
 which I always need to use if I'm doing anything other than posting simple prose.

**It's awesome to type my blog in IntelliJ**.  Do you find yourself trying to use IntelliJ shortcuts in other editors?  The two I
miss the most when I'm not in IntelliJ are Cmd+Y to delete a line, and Ctrl+Shift+J to bring the next line up.  Writing markdown in
IntelliJ with my usual shortcuts (and the [markdown plugin](http://github.com/nicoulaj/idea-markdown)) is really easy and productive.
Plus, of course, you get IntelliJ's ability to paste from any item in the clipboard history. And I don't have to worry about those
random intervals when blogger tells me it hasn't saved my content, and I have no idea if I will just lose hours of work.

**I now own my own content**.  It never really occurred to me before that all the effort I've put into three years of regular blogging is
_out there_, on some Google servers somewhere, and I don't have a copy of that material.  That's dumb,
that doesn't reflect how seriously I take my writing.  Now I have that content here, on my laptop, and it's also backed up in Github,
both as raw markdown and as generated HTML, and versioned.  Massive massive win.

**I have more control over how things are rendered**, and I can customise the display much more.  This has drawbacks though too,
as it's exactly this freedom-to-play that I worry will distract me from actual writing.


As with every project that's worth trying, it wasn't completely without pain.  I followed the (surprisingly excellent) [documentation](http://hugo.spf13.com/overview/introduction),
as well as [these guidelines](http://j3ff.com/blog/building-a-site-with-hugo/), but I did run into some fiddly bits:

1. I couldn't quite get my head around the difference between my [Hugo project code](https://github.com/trishagee/trishagee.com) and my
[actual site content](https://github.com/trishagee/trishagee.github.io) to begin with: how to put them into
 source control and how to get my site on github pages.  I've ended up with two projects on github,
 even though the generated code is technically a subtree of the Hugo project.  I think I'm happy with that.
2. I'm not really sure about the difference between tags, keywords, and topics, if I'm honest.  Maybe this is something I'll grow into.
2. I really need to spend some time on the layout and design, I don't want to simply rip off Steve's original layout.  Plus there are
things I would like to have on the main page which are missing.
2. I needed to convert my old content to the new format
3. Final migration from old to new (incomplete)

To address the last point first, I'm not sure yet if I will take the plunge and do full redirection from Blogger to the new github pages
site (and redirect my domains too), for a while I'm going to run both in parallel and see how I feel.

As for the fourth point, I didn't find a tool for migrating Blogger blogs into markdown that didn't require me to install some other tool
 or language, and there was nothing that was specifically Hugo-shaped, so I surprised myself and did what every programmer would - I
 wrote my own. Surprising because I'm not normally that sort of person - I like to use tools that other people have written,
 I like things that Just Work, I spend all my time coding for my job so I can't be bothered to devote extra time to it.  But my recent
 experiences with [Groovy](http://groovy.codehaus.org/) had convinced me that I could write a simple Groovy parser that would take my exported blog (in Atom XML
 format)
  and turn it into a series of markdown files.  And I was right, I could.  So I've created a new github project,
  [atom-to-hugo](https://github.com/trishagee/atom-to-hugo).  It's very rough, but a) it works and b) it even has tests.  And documentation.

I don't know what's come over me lately, I've been a creative, coding machine.

In summary, I'm pretty happy with the new way of working, but it's going to take me a while to get used to it and decide if it's the way
I want to go.  At the very least, I now have my Blogger content as something markdown-ish.


But there are a couple of things I miss about Blogger:

1. I actually like the way it shows the blog archive on the right hand side, split into months and years.  I use that to motivate me to
blog more if a month looks kinda empty
2. While Google Analytics is definitely more powerful than the simple blogger analytics, I find them an easier way to get a quick insight
 into whether people are reading the blog, and which paths they take to find it.

I don't think either of these are showstoppers, I should be able to work around both of them.