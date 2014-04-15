{
 "disqus_url" : "http://trishagee.github.io/post/getting_started_with_the_mongodb_java_tutorial/",
 "disqus_title" : "Getting started with the MongoDB Java Driver Tutorial",
 "Title": "Getting started with the MongoDB Java Driver Tutorial",
 "Pubdate": "2013-10-24",
 "Keywords": [],
 "Tags": [],
 "Slug": "getting_started_with_the_mongodb_java_tutorial",
 "Section": "resources"
}
Brief guide to running the MongoDB tutorial from QCon London and JAX London.
<!--more-->

## Setup
Create a new work area for this tutorial. For the rest of these instructions I'll refer to it as <code>&lt;location&gt;</code>.  I've put
 mine in <code>~/Documents/workshops/jax</code>

## Installing MongoDB

<a href="http://www.mongodb.org/downloads">Download MongoDB</a> or get it off the USB stick Unzip to an appropriate location,
let's say <code>&lt;location&gt;/mongodb</code>

Then we'll have to create the directory for the data to go into:

<code>cd &lt;location&gt;</code><br /><code>mkdir data</code><br /><div><br /></div>And then start MongoDB:<div>

<code>./mongodb/bin/mongod --dbpath data</code>

Now MongoDB should be running on localhost and port 27017

If you want, you can connect to the shell - this is not necessary for this workshop:

<span style="font-family: monospace;">./mongodb/bin/mongo</span>

## Creating your project
Put [the Java project](https://github.com/trishagee/mongodb-java-tutorial) into <code>&lt;location&gt;/java3.0</code>

<code>cd &lt; location&gt;/java3.0</code>

Run:<br /><code>./gradlew idea</code><br /><div>or</div><code>./gradlew eclipse</code>

Open in your favourite IDE and you should be ready to start playing.

## More help:
<a href="http://docs.mongodb.org/manual/tutorial/">MongoDB Tutorials</a>

## Emergency Gradle Procedure:

<a href="http://www.gradle.org/">Download Gradle</a>&nbsp;or get it off the USB stick<br />Extract to some suitable location. &nbsp;Mine's in&nbsp;<code>/Library/Tools/gradle/</code><br />Put gradle on your path. &nbsp;On the Mac, that means adding the following line to&nbsp;<code>~/.bash_profile</code>:<br /><code>export PATH="/Library/Tools/gradle/bin:$PATH"</code><br /><div><code><br /></code></div></div>
