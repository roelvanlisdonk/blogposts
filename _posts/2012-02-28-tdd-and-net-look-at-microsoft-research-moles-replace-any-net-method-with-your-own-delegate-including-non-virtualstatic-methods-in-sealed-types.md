---
ID: 2505
post_title: >
  How to replace any .NET method with your
  own delegate, including non-virtual /
  static methods in sealed types.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/02/28/tdd-and-net-look-at-microsoft-research-moles-replace-any-net-method-with-your-own-delegate-including-non-virtualstatic-methods-in-sealed-types/
published: true
post_date: 2012-02-28 10:28:12
---
<p align="left">So if you want to use TDD in .NET and use .NET types from for example mscorlib.dll, then you find your self creating interfaces for things like System.IO.File. System.DateTime etc., this is the way you do things in TDD, so the types can be mocked, but this is time consuming. To the rescue comes Microsoft Research with Moles (<a href="http://research.microsoft.com/en-us/projects/moles/">http://research.microsoft.com/en-us/projects/moles/</a>).</p>  <p>&#160;</p>  <p>This allows you to replace any .NET method with your own delegate, including non-virtual / static .NET methods in sealed types, in your test. So production code just uses the .NET types, but in your test you can mock these methods by your own implementations. </p>  <p>Watch the video at: <a href="http://channel9.msdn.com/blogs/peli/moles-replace-any-net-method-with-a-delegate">http://channel9.msdn.com/blogs/peli/moles-replace-any-net-method-with-a-delegate</a></p>