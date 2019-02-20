---
ID: 1787
post_title: 'Setting you&rsquo;re form to show in front with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/10/31/setting-youre-form-to-show-in-front-with-c/
published: true
post_date: 2010-10-31 20:21:42
---
<p>When you want to set you’re form as top most form, when it is hidden behind other windows, you can use the Form property TopMost. After setting the property to true, you should set it to false, so other forms can be the topmost form and stop the flashing of the form in the Windows taskbar.</p>  <pre class="code">TopMost = <span style="color: blue">true</span>;
TopMost = <span style="color: blue">false</span>;</pre>
<a href="http://11011.net/software/vspaste"></a>