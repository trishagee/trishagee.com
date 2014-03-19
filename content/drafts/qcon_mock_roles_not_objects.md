{
 "disqus_url" : "http://trishagee.github.io/post/qcon_mock_roles_not_objects/",
 "disqus_title" : "QCon: Mock Roles, Not Objects",
 "Title": "QCon: Mock Roles, Not Objects",
 "Pubdate": "2007-03-16",
 "Slug": "qcon_mock_roles_not_objects",
 "Section": "post"
}
<a href="http://qcon.infoq.com/qcon/speakers/show_speaker.jsp?oid=171"> Steve Freeman</a>, Independent consultant, M3P<br /><a href="http://qcon.infoq.com/qcon/speakers/show_speaker.jsp?oid=190"> Nat Pryce</a>, Independent consultant, B13<br /><br />- focus the design on the communications<br />- how do we unit test this?<br />- TODO: go back to KI and write the tests properly<br />- "Mockery" contains neighborhood of thing we're testing - stuff that's local to it<br />- TODO: check if the bank supports JMock<br />- Annotations again<br />- Check out <a href="http://qcon.infoq.com/qcon/file?path=/QCon2007/slides/NatPryce_Freeman_Synaesthesis.pdf">slides for this presentation</a><br />- The code doesn't seem to have assertions and I wondered if JMock was doing all the work<br />- Too many params in constructors is potentially brittle<br />-&nbsp;&nbsp;&nbsp;&nbsp; - might be better to initialise deffault values in constructor and provide setters<br />- Integration tests for shell round 3rd party libraries, but doesn't mock 3rd parties<br />- TODO: Split KI into integration and unit tests - DAOs are integration<br />- Don't forget if your tests are hard you're doing something wrong<br />- Error log is actually a UI - it's an interface to the sys-admin user.&nbsp; Worth bearing that in mind when you're logging errors and/or testing logging.
