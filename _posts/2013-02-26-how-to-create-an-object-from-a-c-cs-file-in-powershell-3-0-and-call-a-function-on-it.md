---
ID: 3173
post_title: 'How to create an object from a C# *.cs file in PowerShell 3.0 and call a function on it.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/02/26/how-to-create-an-object-from-a-c-cs-file-in-powershell-3-0-and-call-a-function-on-it/
published: true
post_date: 2013-02-26 11:27:16
---
<p>If you want to create an object based on the C# code in a *.cs file, by using PowerShell 3.0 you can use the following C# and PowerShell code:</p>  <p>&#160;</p>  <p><strong>Create a folder &quot;C:\Temp&quot;</strong></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image5.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image_thumb5.png" width="580" height="208" /></a></p>  <p>&#160;</p>  <p><strong>C# MyClass.cs file</strong></p>  <pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Diagnostics;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">MyNameSpace
{
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">MyClass
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">MyFunction()
        {
            </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;Hello from MyNameSpace.MyClass.MyFunction.&quot;</span><span style="background: white; color: black">);
        }
    }
}
    </span></pre>

<p>&#160;</p>

<p><strong>PowerShell Execute_MyNamespace_MyClass_MyFunction.ps1</strong></p>

<pre class="code"> <span style="color: blue">Add-Type </span><span style="color: navy">-Path </span><span style="color: darkred">&quot;C:\Temp\MyClass.cs&quot;
</span><span style="color: #ff4500">$labeler </span><span style="color: #a9a9a9">= </span><span style="color: blue">New-Object </span><span style="color: #8a2be2">MyNameSpace.MyClass
</span><span style="color: #ff4500">$labeler</span><span style="color: #a9a9a9">.</span>MyFunction()
<span style="color: blue">pause 
</span></pre>
<strong></strong>

<p><strong>Execute</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image6.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image_thumb6.png" width="580" height="215" /></a></p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image7.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image_thumb7.png" width="580" height="138" /></a></p>