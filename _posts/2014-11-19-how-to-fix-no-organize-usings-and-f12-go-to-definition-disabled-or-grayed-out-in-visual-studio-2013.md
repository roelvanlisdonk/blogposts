---
ID: 4147
post_title: 'How to Fix: No &ldquo;organize usings&rdquo; and F12 &ldquo;Go to definition&rdquo; disabled or grayed out in Visual Studio 2013'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/11/19/how-to-fix-no-organize-usings-and-f12-go-to-definition-disabled-or-grayed-out-in-visual-studio-2013/
published: true
post_date: 2014-11-19 08:51:09
---
<p>When I right clicked on my using statements in a C# file, the context edit menu, didn’t contain the options for refactoring and “organize usings” and the menu item “F12 Go to definition” was grayed out.</p>  <p>I found the fix at: <a title="http://stackoverflow.com/questions/25898616/visual-studio-go-to-definition-disabled-or-gray-out" href="http://stackoverflow.com/questions/25898616/visual-studio-go-to-definition-disabled-or-gray-out">http://stackoverflow.com/questions/25898616/visual-studio-go-to-definition-disabled-or-gray-out</a></p>  <p>&#160;</p>  <ul>   <li>Clean your solution</li>    <li>Close solution</li>    <li>Remove any [solution].ncb, [solution].suo, [solution].vspscc files</li>    <li>Reopen solution</li>    <li>Rebuild solution</li> </ul>  <p>Menu options should appear and be enabled.</p>