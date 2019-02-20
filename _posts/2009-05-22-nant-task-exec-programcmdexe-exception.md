---
ID: 441
post_title: 'NANT task &lt;exec program=&quot;CMD.EXE&quot; exception:'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/nant-task-exec-programcmdexe-exception/
published: true
post_date: 2009-05-22 14:20:29
---
When you use NANT to execute a bat file, use the &lt;arg ... /&gt; tag to set parameters and use the workingdir to change the current path location, like:  <br />  <br />  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">exec </span><span style="color: red">program</span><span style="color: blue">=</span>&quot;<span style="color: blue">CMD.EXE</span>&quot; <span style="color: red">commandline</span><span style="color: blue">=</span>&quot;<span style="color: blue">/C DatabaseInstallation.cmd</span>&quot; <span style="color: red">workingdir</span><span style="color: blue">=</span>&quot;<span style="color: blue">${installPath}</span>&quot;<span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_ServerInstanceName}</span>&quot; <span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_Name}</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_Domain}</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_DtsPackagesFolder}</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">exec</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<br />If you use it like:

<br />

<br />

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">exec </span><span style="color: red">program</span><span style="color: blue">=</span>&quot;<span style="color: blue">CMD.EXE</span>&quot; <span style="color: red">commandline</span><span style="color: blue">=</span>&quot;<span style="color: blue">/C <span style="color: blue">${installPath}</span>\DatabaseInstallation.cmd</span>&quot; <span style="color: red">workingdir</span><span style="color: blue">=</span>&quot;<span style="color: blue">${installPath}</span>&quot;<span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_ServerInstanceName}</span>&quot; <span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_Name}</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_Domain}</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_DtsPackagesFolder}</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">exec</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>You will get the exception:

<br />

<br />

<p>&#160;&#160;&#160;&#160; [exec] 'C:\Program' is not recognized as an internal or external command,
  <br />&#160;&#160;&#160;&#160; [exec] operable program or batch file. </p>

<p>BUILD FAILED - 0 non-fatal error(s), 2 warning(s)</p>
This can occur even if you use quotes:

<br />

<br />

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">exec </span><span style="color: red">program</span><span style="color: blue">=</span>&quot;<span style="color: blue">CMD.EXE</span>&quot; <span style="color: red">commandline</span><span style="color: blue">=</span>&quot;<span style="color: blue">/C &amp;quot;<span style="color: blue">${installPath}</span>\DatabaseInstallation.cmd&amp;quot;</span>&quot; <span style="color: red">workingdir</span><span style="color: blue">=</span>&quot;<span style="color: blue">${installPath}</span>&quot;<span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_ServerInstanceName}</span>&quot; <span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_Name}</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_Domain}</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">arg </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">${Database_DtsPackagesFolder}</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">exec</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>