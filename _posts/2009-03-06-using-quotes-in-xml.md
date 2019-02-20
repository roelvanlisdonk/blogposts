---
ID: 263
post_title: Using quotes in XML
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/06/using-quotes-in-xml/
published: true
post_date: 2009-03-06 10:26:03
---
<p>To use quotes in xml, use "<span style="color:red;">&amp;quot;</span>"</p><pre class="code"><span style="color:blue;"></span></pre><pre class="code"><span style="color:blue;">&lt;</span><span style="color:#a31515;">exec </span><span style="color:red;">program</span><span style="color:blue;">=</span>"<span style="color:blue;">CMD.EXE</span>"
              <span style="color:red;">commandline</span><span style="color:blue;">=</span>"<span style="color:blue;">/C </span><span style="color:red;">&amp;quot;</span><span style="color:blue;">${installPath}\DatabaseInstallation.cmd</span><span style="color:red;">&amp;quot;</span>"
              <span style="color:red;">workingdir</span><span style="color:blue;">=</span>"<span style="color:blue;">${installPath}</span>"<span style="color:blue;">&gt;
            &lt;</span><span style="color:#a31515;">arg </span><span style="color:red;">value</span><span style="color:blue;">=</span>"<span style="color:blue;">${Database_DataSource}</span>" <span style="color:blue;">/&gt;</span></pre><a href="http://11011.net/software/vspaste"></a>