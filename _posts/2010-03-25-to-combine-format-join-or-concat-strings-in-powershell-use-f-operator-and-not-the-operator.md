---
ID: 1153
post_title: >
  To combine, format, join or concat
  strings in PowerShell
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/25/to-combine-format-join-or-concat-strings-in-powershell-use-f-operator-and-not-the-operator/
published: true
post_date: 2010-03-25 12:04:52
---
<p>You can concat strings in PowerShell by using the + operator, but like in C#, I think it is better to use a formatting approach by using the –f string operator:</p>  <p>&#160;</p>  <p><strong>[-f operator]</strong></p>  <p>PS C:\Users\rLisdonk&gt; &quot;My computer {0} has {1} MB of memory.&quot; -f &quot;L001&quot;, &quot;4096&quot;   <br />My computer L001 has 4096 MB of memory.</p>  <p>&#160;</p>  <p><strong>[Double quoted string with variables]</strong></p>  <p>You could also use variables in the double quoted string, like:</p>  <p>$myComputer = “L001”</p>  <p>$memory = “4096”</p> PS C:\Users\rLisdonk&gt; &quot;My computer $myComputer has $memory MB of memory.&quot;  <p>&#160;</p>  <p><strong>[+= operator]</strong></p>  <p>You could also use += operator to concat strings</p>  <p>PS C:\Users\rLisdonk&gt; $test = &quot;This is a &quot;   <br />PS C:\Users\rLisdonk&gt; $test += &quot;test string&quot;    <br />PS C:\Users\rLisdonk&gt; $test    <br />This is a test string</p>  <p>&#160;</p>  <p><strong>[Escape characters]</strong></p>  <p>see <a title="http://www.techotopia.com/index.php/Windows_PowerShell_1.0_String_Quoting_and_Escape_Sequences" href="http://www.techotopia.com/index.php/Windows_PowerShell_1.0_String_Quoting_and_Escape_Sequences">http://www.techotopia.com/index.php/Windows_PowerShell_1.0_String_Quoting_and_Escape_Sequences</a></p>