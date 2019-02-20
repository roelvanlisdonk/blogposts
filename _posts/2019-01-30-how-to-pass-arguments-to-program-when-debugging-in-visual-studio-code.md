---
ID: 5333
post_title: >
  How to pass arguments to program, when
  debugging in Visual Studio Code
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2019/01/30/how-to-pass-arguments-to-program-when-debugging-in-visual-studio-code/
published: true
post_date: 2019-01-30 07:13:22
---
Found my answer at: <a href="https://github.com/Microsoft/vscode/issues/2167">https://github.com/Microsoft/vscode/issues/2167</a>

<p style="background: white"><span style="color:#24292e; font-family:Segoe UI; font-size:10pt">You have to pass the arguments as individual string elements:
</span>

<p style="background: #f6f8fa"><span style="color:#032f62; font-family:Consolas; font-size:9pt">"args"<span style="color:#24292e">: [
</span></span>

<p style="background: #f6f8fa"><span style="color:#24292e; font-family:Consolas; font-size:9pt">
<span style="color:#032f62">"--test"<span style="color:#24292e">, <span style="color:#032f62">"buildOutput/JavaScript1.js"<span style="color:#24292e">,
</span></span></span></span></span>

<p style="background: #f6f8fa"><span style="color:#24292e; font-family:Consolas; font-size:9pt">
<span style="color:#032f62">"--env"<span style="color:#24292e">, <span style="color:#032f62">"devtest-chrome-win8"<span style="color:#24292e">
</span></span></span></span></span>

<p style="background: #f6f8fa"><span style="color:#24292e; font-family:Consolas; font-size:9pt">]
</span>

My program needed a parameter -d and a parameter -s, so I changed the args to:

<p style="background: #f6f8fa"><span style="color:#032f62; font-family:Consolas; font-size:9pt">"args"<span style="color:#24292e">: [
</span></span>

<p style="background: #f6f8fa"><span style="color:#24292e; font-family:Consolas; font-size:9pt">
<span style="color:#032f62">"-d"<span style="color:#24292e">, <span style="color:#032f62">"some value for d"<span style="color:#24292e">,
</span></span></span></span></span>

<p style="background: #f6f8fa"><span style="color:#24292e; font-family:Consolas; font-size:9pt">
<span style="color:#032f62">"-s"<span style="color:#24292e">, <span style="color:#032f62">"some value for s"<span style="color:#24292e">
</span></span></span></span></span>

<p style="background: #f6f8fa"><span style="color:#24292e; font-family:Consolas; font-size:9pt">]
</span>

And those parameters where picked up by the McMaster.Extensions.CommandLineUtils, that I used in the program.