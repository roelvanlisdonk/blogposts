---
ID: 1156
post_title: 'How to call a PowerShell script with named parameters from a PowerShell (*.ps1) script'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/25/how-to-call-a-powershell-script-with-named-parameters-from-a-powershell-ps1-script/
published: true
post_date: 2010-03-25 15:24:05
---
<p>If you want to call a PowerShell script (Test2.ps1) with named parameters from a PowerShell script (Test1.ps1), you <strong>can’t</strong> use the &amp; operator, like &amp; “C:\Temp\Test2.ps1” –Computer L001 –User User1, because the &amp; command is an alias for the Get-Command cmdlet. The Get-Command cmdlet executes precisely one command, see : <a title="http://powershell.com/cs/blogs/ebook/archive/2009/03/30/chapter-12-command-discovery-and-scriptblocks.aspx#the-call-operator-quotampquot" href="http://powershell.com/cs/blogs/ebook/archive/2009/03/30/chapter-12-command-discovery-and-scriptblocks.aspx#the-call-operator-quotampquot">http://powershell.com/cs/blogs/ebook/archive/2009/03/30/chapter-12-command-discovery-and-scriptblocks.aspx#the-call-operator-quotampquot</a>, but you can use script blocks to execute more then one command or the Invoke-Expression cmdlet. I used the Invoke-Expression cmdlet to call a PowerShell script with named parameters from an other PowerShell script.    <br />    <br />    <br /><strong>[Test1.ps1]</strong></p>  <p>$command = “C:\Temp\Test2.ps1” –Computer L014 –User User1</p>  <p>Invoke-Expression $command</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>[Test2.ps1]</strong></p>  <p>param   <br />(    <br />&#160;&#160;&#160; [string]$Computer = &quot;MyDefaultComputer&quot;,    <br />&#160;&#160;&#160; [string]$User = &quot;MyDefaultUser&quot;</p>  <p>)</p>  <p>$Computer</p>  <p>$User</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>[Result]</strong></p>  <p>L014</p>  <p>User1</p>