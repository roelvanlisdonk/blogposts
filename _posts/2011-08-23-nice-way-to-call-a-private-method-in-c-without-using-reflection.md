---
ID: 2135
post_title: 'Nice way to call a private method in C# without using &ldquo;reflection&rdquo;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/08/23/nice-way-to-call-a-private-method-in-c-without-using-reflection/
published: true
post_date: 2011-08-23 14:57:29
---
<p>&#160;</p>  <p><a title="http://elegantcode.com/2010/01/28/calling-non-public-methods/" href="http://elegantcode.com/2010/01/28/calling-non-public-methods/">http://elegantcode.com/2010/01/28/calling-non-public-methods/</a></p>  <p>&#160;</p>  <p>// Calling code that uses delegates </p>  <p>var subject = new Subject(); </p>  <p>var doSomething = (Func&lt;String, String&gt;) </p>  <p>Delegate.CreateDelegate(typeof(Func&lt;String, String&gt;), subject, &quot;DoSomething&quot;); </p>  <p>Console.WriteLine(doSomething(&quot;Hello Freggles&quot;));</p>  <p>&#160;</p>  <p>Note that this only works for instance methods and not for static methods. </p>