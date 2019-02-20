---
ID: 780
post_title: 'Use &#8216;/&#8217; and not &#8216;\&#8217; to link style sheet in subfolders, else Firefox won&#8217;t load CSS.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/20/use-and-not-to-link-style-sheet-in-subfolders-else-firefox-wont-load-css/
published: true
post_date: 2009-10-20 11:12:08
---
<p>If you use a subfolder Css containing all you’re css files, use forward slash to link the CSS file, else Firefox won’t load the CSS file.</p>  <pre class="code">So, use:<br /><br /><br /></pre>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">link </span><span style="color: red">href</span><span style="color: blue">=&quot;Css/Master.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>