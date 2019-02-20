---
ID: 2751
post_title: 'TIP: Reassign keyboard shortcuts, when using TDD with Microsoft Visual Studio and TestDriven.Net'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/07/03/tip-reassign-keyboard-shortcuts-when-using-tdd-with-microsoft-visual-studio-and-testdriven-net/
published: true
post_date: 2012-07-03 09:42:54
---
<p>If you are using TDD in Microsoft Visual Studio 2010 and apply that red – green – refactor thingie, you want your tests to execute as fast as possible. Well MSTEST in Microsoft Visual Studio 2010 is known to be a snail, so for TDD in Microsoft Visual Studio 2010 you probably want to use external tools like ReSharper, TestDriven.Net&#160; etc.</p>  <p>&#160;</p>  <p>To further improve the speed I reassign the keyboard shortcuts:</p>  <ul>   <li>CTRL + Q to run the current test(s) in context without debugger.</li>    <li>CTRL + W to run the current test(s) in context with debugger.</li> </ul>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/07/image.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/07/image_thumb.png" width="580" height="340" /></a></p>  <p>&#160;</p>  <p><strong>Notes</strong></p>  <ul>   <li>By the way, in Microsoft Visual Studio 2012 there is a tremendous performance improvement in running unit test, so you might want to look at that.</li>    <li>An other tip: don’t use CTRL + S (to save code), instead use CTRL + Q to save, compile and run tests on your code at once.</li> </ul>