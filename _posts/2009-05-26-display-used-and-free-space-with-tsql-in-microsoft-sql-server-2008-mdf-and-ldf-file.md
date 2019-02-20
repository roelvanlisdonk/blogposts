---
ID: 499
post_title: >
  Display used and free space with TSQL in
  Microsoft SQL Server 2008 mdf and ldf
  file
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/26/display-used-and-free-space-with-tsql-in-microsoft-sql-server-2008-mdf-and-ldf-file/
published: true
post_date: 2009-05-26 11:01:20
---
<p>   <br />To calculate the &quot;size&quot;, &quot;used size in&quot; and &quot;free space in&quot; a Microsoft SQL Server 2008 mdf or ldf file use:</p>  <pre class="code"><span style="color: blue">use master<br /><br /><font color="#000000">go<br /></font>select
    </span>name<span style="color: gray">,
    </span><span style="color: magenta">cast</span><span style="color: gray">((</span>size<span style="color: gray">/</span>128.0<span style="color: gray">) </span><span style="color: blue">as int</span><span style="color: gray">) </span><span style="color: blue">as </span>TotalSpaceInMB<span style="color: gray">,
    </span><span style="color: magenta">cast</span><span style="color: gray">((</span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: magenta">fileproperty</span><span style="color: gray">(</span>name<span style="color: gray">, </span><span style="color: red">'SpaceUsed'</span><span style="color: gray">) </span><span style="color: blue">as int</span><span style="color: gray">)/</span>128.0<span style="color: gray">) </span><span style="color: blue">as int</span><span style="color: gray">) </span><span style="color: blue">as </span>UsedSpaceInMB<span style="color: gray">,
    </span><span style="color: magenta">cast</span><span style="color: gray">((</span>size<span style="color: gray">/</span>128.0 <span style="color: gray">- </span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: magenta">fileproperty</span><span style="color: gray">(</span>name<span style="color: gray">, </span><span style="color: red">'SpaceUsed'</span><span style="color: gray">) </span><span style="color: blue">AS int</span><span style="color: gray">)/</span>128.0<span style="color: gray">) </span><span style="color: blue">as int</span><span style="color: gray">) </span><span style="color: blue">as </span>FreeSpaceInMB
<span style="color: blue">from
    </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">database_files</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p><strong>Result</strong>

  <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image11.png"><img style="border-bottom: 0px; border-left: 0px; border-top: 0px; border-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image-thumb11.png" width="333" height="105" /></a>&#160; <br />

  <br />

  <br />For more information on <span style="color: magenta">fileproperty</span>, see: <a title="http://msdn.microsoft.com/en-us/library/ms188401.aspx" href="http://msdn.microsoft.com/en-us/library/ms188401.aspx">http://msdn.microsoft.com/en-us/library/ms188401.aspx</a></p>