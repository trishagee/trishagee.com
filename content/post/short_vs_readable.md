{
    "disqus_url" : "http://trishagee.github.io/post/short_vs_readable.md",
    "disqus_title" : "Succinct vs Readable",
        "Title": "Readable, Succinct, or Just Plain Short?",
    "Pubdate": "2014-07-02",
    "Keywords": ["groovy", "code"],
    "Tags": ["groovy", "code"],
    "Slug": "short_vs_readable.md",
    "Section": "post"
}

Which is more readable?

    releaseVersion = version.substring(0, version.indexOf('-SNAPSHOT'))

or

    releaseVersion = version[0..-10]
 
<!--more-->
 
Given a value of `0.109-SNAPSHOT` for `version`, they both give the same result.  And I'm tempted by the second, 
because it's shorter.  But I'm going to go with the first one - not because it's more Java-ish and I'm scared of Groovy syntax, 
but because it's easier to understand if/when something goes wrong.

For example: if `version` doesn't conform to the expected pattern, the two code fragments fail in two different ways.  If `version` 
doesn't contain `-SNAPSHOT`, the first will fail with:

    java.lang.StringIndexOutOfBoundsException: String index out of range: -1
    
whereas the second will either arbitrarily slice the last 9 characters off the end of whatever the String does contain, 
or if it's too short you'll get something like:

    java.lang.ArrayIndexOutOfBoundsException: Negative array index [-10] too large for array size 5

When you, the developer, see this error (or notice your mangled version number) and look at the failing line of code, 
you'll have two different experiences.  When looking at the second example, if you didn't write it in the first place or if you have a 
memory as shocking as mine, you won't get any clues from that code as to what the _purpose_ is - you'll see what it does (chop the last 
9 characters off the `version` string), but not why.  You can "fix" the problem by adding an arbitrary 9 characters onto your `version`. 

If you're looking at the first example, however, you'll see the intent right there - it's trying to chop the string `-SNAPSHOT` (and any
characters that might happen to come after it) off the end of the `version` string.  With this line of code, 
if you checked the value of `version` and saw it didn't have the correct suffix, you'd have a good idea of what the problem is and how 
to solve it.

There's a third way, that potentially keeps the descriptiveness (is that a word?) of the first solution and makes it a bit shorter and 
Groovier:

    releaseVersion = version[0..<version.indexOf('-SNAPSHOT')]

You need the less-than sign plonked in there to make it work correctly, which I find a bit jarring, 
but it does work.  It's a little more succinct than the original Java syntax and retains the intent.
 
So in conclusion: yes, shorter code is generally better (and often more readable).  But I don't believe in sacrificing code that 
expresses the intent in order to reduce the number of characters used.  We're not living in a memory-poor world any more, 
and code is meant to be read by humans as well as computers.  Let's make our code easy to understand when it goes wrong, 
not simply the shortest way to do something when the stars are all perfectly aligned.

