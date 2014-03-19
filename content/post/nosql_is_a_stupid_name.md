{
 "disqus_url" : "http://trishagee.github.io/post/nosql_is_a_stupid_name/",
 "disqus_title" : "NoSQL is a Stupid Name",
 "Title": "NoSQL is a Stupid Name",
 "Pubdate": "2012-10-23",
 "Slug": "nosql_is_a_stupid_name",
 "Section": "post"
}
<div style="float:left; margin-right: 10px;"><script type="text/javascript">var dzone_url = 'http://java.dzone.com/articles/nosql-stupid-name';</script><script type="text/javascript">var dzone_title = 'NoSQL is a Stupid Name';</script><script type="text/javascript">var dzone_blurb = '[description]';</script><script type="text/javascript">var dzone_style = '1';</script><script language="javascript" src="http://widgets.dzone.com/links/widgets/zoneit.js"></script></div>So, I've finished my first full week in the new job and I've learnt lots of new stuff.  Which is great, because that's usually why you change jobs.<br /><br /><div>I'm learning a lot about these new-fangled <a href="http://nosql-database.org/">NoSQL</a> database thingies.  The <a href="http://martinfowler.com/articles/lmax.html">LMAX architecture</a> was based on keeping everything in memory and reducing the waits for IO - messages were journalled to disk, and reads and writes to the MySQL database were off the critical path.  Therefore doing anything radical to the storage side of the architecture was just not high on the list of priorities.<br /><br /></div><div>Everything I knew about NoSQL I learnt from the various conferences I've been going to in the last year, and even then that's limited - without a business reason to pursue knowledge I know it'll just leak out of my brain, so I avoid sessions with no immediate applicability to me.<br /><br /></div><div>Let's summarise what I knew about NoSQL databases before last week:<br /><ul><li>They don't use SQL.  Who knew?&nbsp;</li><li>There are different flavours. &nbsp;There's a graphy one and key-value things and... others...</li><li>They're "scalable" (yes, yes, it's <a href="http://www.mongodb-is-web-scale.com/">web scale</a>).&nbsp;</li><li>Some/many/all(?) embrace the idea of eventual consistency&nbsp;</li></ul><br />I was suspicious of the hype surrounding NoSQL, partly because it's associated with the meaningless marketing term "Big Data" and partly because I'm a cynic that sneers at things that get too popular.  Here's what I think when I hear the following terms:<br /><ul><li><i>Cloud</i> - Fire your systems people and ditch your comms room!</li><li><i>Big Data</i> - Parse Twitter in order to learn how to read your customer's minds!</li><li><i>NoSQL</i> - Stop paying Oracle!</li><li><i>Functional</i> - We couldn't get good enough at mainstream programming languages so we switched to something more difficult!</li></ul><br />I don't know if it's healthy to be this cynical, but I'm too old to jump on every bandwagon that comes along.<br /><i><br /></i><i>Anyway</i>. Back to the people who now pay my bills.<br /><div><br /></div>It's unfortunate that the lack of SQL is the thing that captured the imagination, rather than the lack of tables and a relational structure.  SQL was never (in my mind) a particularly evil thing, it's a pretty good language for saying "I want this stuff from this place that fits these criteria", and that's something we're going to have to do at some point whatever the technology.<br /><br /></div><div>It's rather more important that it's the structure of the data that's different in NoSQL databases.</div><div><br />In a traditional relational databases you have tables, and relationships between those tables are achieved with foreign keys.  I'm starting to think of these as something kind of grid-shaped with links between them:<br /><br /><table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto;"><tbody><tr><td style="text-align: center;"><a href="http://2.bp.blogspot.com/-6nq0Sj37TrM/UIZ3pM-gV0I/AAAAAAAALPQ/1UDd1SgnHt8/s1600/Relational.png" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="240" src="http://2.bp.blogspot.com/-6nq0Sj37TrM/UIZ3pM-gV0I/AAAAAAAALPQ/1UDd1SgnHt8/s320/Relational.png" width="320" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">Series of database tables and their relationships. &nbsp;Honest.</td></tr></tbody></table>(Yes, I'm experimenting again. This time with my shiny new iPad, a stylus and <a href="https://itunes.apple.com/gb/app/penultimate/id354098826?mt=8">Penultimate</a>. It's good for ad-hoc drawings, but lacks the precision of the graphics tablet and flexibility of GIMP).<br /><br /></div>At the very high level, it seems like there are four (ish) types of NoSQL databases: <br /><ol><li>Column Family&nbsp;</li><li>Key/Value&nbsp;</li><li>Graph&nbsp;</li><li>Document&nbsp;</li></ol><b>Column Family</b><br />Column family databases feel to me, as a newbie to the field, similar to key/value, which I'll come on to. I've mostly heard <a href="http://cassandra.apache.org/">Cassandra</a> used as an example of this type of NoSQL database. I guess the way I think of this, and of course I could be wrong/over-simplifying, is a unique key linked to a set of key/values:<br /><br /><script src="https://gist.github.com/3938260.js?file=gistfile1.txt"></script> <br />Which I'm translating into groups of key/value pairs, with a the ID as a sort of header: <br /><table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto;"><tbody><tr><td style="text-align: center;"><a href="http://3.bp.blogspot.com/-Xexa2Oo1KjI/UIZ4miTPudI/AAAAAAAALPY/ZCxFVbTpsRk/s1600/ColumnFamily2.png" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="145" src="http://3.bp.blogspot.com/-Xexa2Oo1KjI/UIZ4miTPudI/AAAAAAAALPY/ZCxFVbTpsRk/s320/ColumnFamily2.png" width="320" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">Key/value pairs grouped by ID</td></tr></tbody></table>You need the key in order to look up all the details about me.  The way I hear it, it's great for writing data, but it's less flexible for ad-hoc queries.  <br /><br /><b>Key/Value</b><br />These types of NoSQL database (e.g. <a href="http://docs.basho.com/riak/latest/">Riak</a>) are pretty much as schema-less as you get - just dump key-value pairs into them.  To be honest, the best description I found was on <a href="http://dba.stackexchange.com/questions/607/what-is-a-key-value-store-database">dba.stackexchange.com</a>, so I'm not going to re-write that with my (at this point) limited understanding.  <br /><table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;"><a href="http://1.bp.blogspot.com/-puUC12LdQkg/UIZ48Oiw4FI/AAAAAAAALPg/mrMKn8PWCw8/s1600/KeyValue.png" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="200" src="http://1.bp.blogspot.com/-puUC12LdQkg/UIZ48Oiw4FI/AAAAAAAALPg/mrMKn8PWCw8/s200/KeyValue.png" width="125" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">Never ending lists of key/values</td></tr></tbody></table>From what I've heard so far, both Key/Value and Column Family databases embrace <a href="http://en.wikipedia.org/wiki/Eventual_consistency">eventual consistency</a>.  I don't know how much of that is a function of their data model and how much is decided by the individual products.  For some people eventual consistency is deal-breaker, but in many cases it seems to me that it's just a matter of getting your head around this and designing your application appropriately.<br /><br /><b>Graph</b><br />I came across graph databases when I stumbled across <a href="http://neo4j.org/">Neo4j</a>, chatting to some of the very smart guys there.  A graph database lets you model you data as a series of nodes and relationships.  And if I think about it, this is not a massive step from either relational models <i>or</i> object models.  It doesn't just apply well to the social networking domain (where it's very easy to think in terms of users and their relationships), in actual fact lots of things we design could be modelled this way.  Not having used it, I'm not sure just how much of a mental leap you need to take to start thinking that way, but it seems like it might be a good fit for many problems. <br /><table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;"><a href="http://3.bp.blogspot.com/-RTpXIRNJm5M/UIZ5IS5n3ZI/AAAAAAAALPo/cer-1dsRSXs/s1600/Graph.png" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="188" src="http://3.bp.blogspot.com/-RTpXIRNJm5M/UIZ5IS5n3ZI/AAAAAAAALPo/cer-1dsRSXs/s200/Graph.png" width="200" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">Graph of nodes with annotated relationships</td></tr></tbody></table>I'd be interested in what the architectural trade-offs in using this model are.<br /><br /><b>Document<br /><span class="Apple-style-span" style="font-weight: normal;">Now MongoDB falls into category four, the document database.  And as a NoSQL <span class="Apple-style-span" style="font-family: 'Courier New', Courier, monospace;">n00b</span>, this is now the product and area I know most about, and am clearly going to be more excited about since <a href="http://www.10gen.com/">10gen</a> are indoctrinating me in the MongoDB way.</span></b><br /><b><span class="Apple-style-span" style="font-weight: normal;"><br /></span></b>Documents are a familiar structure for developers, especially if they've been working with JSON.  So, a document might be:<br /><br /><script src="https://gist.github.com/3938248.js?file=gistfile1.txt"></script> <br />To me, this looks like it maps onto to my domain-shaped Object Model more easily than a relational database, which always needs some sort of O-R mapping (whether you do this with hibernate or use Spring to do it yourself, you're still mapping tables into objects and vice versa).  What I like about the document format is the nested sub-documents for data that belongs together.  In relational databases you often end up denormalising for performance anyway, so why not just accept that up front and have it as part of the thing you're storing?<br /><br /><table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;"><a href="http://1.bp.blogspot.com/-1bL7VJuNNg4/UIaA2mq8jZI/AAAAAAAALQA/KWM3_1Mzr7A/s1600/Document1.png" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="200" src="http://1.bp.blogspot.com/-1bL7VJuNNg4/UIaA2mq8jZI/AAAAAAAALQA/KWM3_1Mzr7A/s200/Document1.png" width="163" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">A document with sub-documents. &nbsp; &nbsp;Think XML/JSON.</td></tr></tbody></table>This does have a cost, of course - nothing is without trade-offs.  Every time you request this document, you get the whole lot.  You can't have the person without the address.  So, you do need to understand the relationships (still) and whether you're usually going to want to get all that data at the same time or whether you might want to make two separate calls.<br /><br />Which brings me on to another thing which is familiar from relational days - foreign keys.  A field in your document can be the ID of another document, so you can follow the links through and retrieve other documents associated with the starting one.  Again, there are trade-offs here - each link you follow is a different request to the database.  These database requests can be very quick, but if you wanted this data every time, you'd probably want it embeded in your first document to save the additional call.  I guess it's a latency vs throughput question really - a single query which returns a chunky document, or multiple queries that return smaller ones.<br /><br /><table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;"><a href="http://1.bp.blogspot.com/-VhPGWfgeWt0/UIaJ4gXvdgI/AAAAAAAALQg/kSnNli89oIw/s1600/Document2.png" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="194" src="http://1.bp.blogspot.com/-VhPGWfgeWt0/UIaJ4gXvdgI/AAAAAAAALQg/kSnNli89oIw/s320/Document2.png" width="320" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">Documents can link to other documents.</td></tr></tbody></table>So schema design is still important in document databases even if you don't have a relational schema.  No new technology is an excuse to stop thinking about the problem you're trying to solve and understanding the tradeoffs in design.<br /><br />One of the advantages, it seems, of something like MongoDB over some of the key/value databases is the ability to write ad-hoc queries and to tune for those queries.  The data is structured (it's in a document) and it doesn't have to be in the same structure every time - not every document relating to a person needs all the fields that another person might have.  But you can still query for people who have blue cars or people who live in London, or people who's surnames begin with G.  If you find yourself doing the same query a number of times, you can add indexes to MongoDB the same way you would a relational database.<br /><br />Semms like I'm getting into more of the nitty-gritty MongoDB details, so I'll stop there and leave that for another time.<br /><br /><b>In Summary</b><br />Classing a whole swathe of products as "NoSQL" is misleading and confusing. &nbsp;The only thing they all share in common is that they are not traditional relational databases. &nbsp;Other than that, some of them are as different from each other as they are from relational databases. &nbsp;I haven't even mentioned caching technologies - these products have functionality which overlaps with NoSQL databases as well. &nbsp;But even then, the purposes are somewhat different, and not even mutually exclusive.<br /><br />As with anything, it's really important to understand the strengths and weaknesses of a technology, and the demands of your domain. &nbsp;These different ways of organising data, and different products, are going to perform really well in certain circumstances, and pretty poorly when used in others. &nbsp;Getting an understanding of what those strengths and weaknesses are is going to be important in making the correct product/architecture/design decisions.<br /><br />None of this information is new, there's a lot of material on the web about the different types of NoSQL databases. I'm writing it more for my own benefit than anything else, my memory is notoriously shocking. &nbsp;For more in-depth (and probably more accurate reading) there's:<br /><ul><li>Martin Fowler's <a href="http://www.amazon.com/gp/product/B0090J3SYW/ref=as_li_qf_sp_asin_tl?ie=UTF8&amp;camp=1789&amp;creative=9325&amp;creativeASIN=B0090J3SYW&amp;linkCode=as2&amp;tag=trissramb-20">NoSQL Distilled</a><img alt="" border="0" height="1" src="http://www.assoc-amazon.com/e/ir?t=trissramb-20&amp;l=as2&amp;o=1&amp;a=B0090J3SYW" style="border: none !important; margin: 0px !important;" width="1" /></li><li>...and his <a href="http://martinfowler.com/articles/nosql-intro.pdf">introduction to the subject</a></li><li>Tim Berglund (@tlberglund) did a great overview of three types at JAX London last week. &nbsp;There's a video of the same content (different conference) <a href="http://vimeo.com/51660128">here</a>.</li><li><a href="http://nosql-database.org/">http://nosql-database.org/</a>&nbsp;appears to list all the products that fall under the massive umbrella, but isn't the most usable of sites.</li><li>And yes, I used Wikipedia. &nbsp;Which is probably where I went wrong...</li></ul>