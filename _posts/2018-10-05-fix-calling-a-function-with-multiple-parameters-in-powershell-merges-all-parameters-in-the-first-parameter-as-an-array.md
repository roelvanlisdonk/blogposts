---
ID: 5265
post_title: 'Fix: Calling a function with multiple parameters in PowerShell, merges all parameters in the first parameter as an array'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/10/05/fix-calling-a-function-with-multiple-parameters-in-powershell-merges-all-parameters-in-the-first-parameter-as-an-array/
published: true
post_date: 2018-10-05 15:34:22
---
<p>
 </p><p>When you call a PowerShell function, that expects multiple parameters, with parenthesis, all parameters will be merged in the first parameter, as an array.
</p><p>The solution is, to call the function with named parameters.
</p><p>So NOT JoinText($p1, $p2, $p3) but JoinText -p1 $p1 -p2 $p2 -p3 $p3
</p><p>
 </p><p><strong>script1.ps1
</strong></p><p>function JoinText([string]$p1, [string]$p2, [string]$p3) {
</p><p>    return "$p1 $p2 $p3"
</p><p>}
</p><p>
 </p><p><strong>script2-wrong.ps1
</strong></p><p>$p1 = "some text 1"
</p><p>$p2 = "some text 2"
</p><p>$p3 = "some text 3"
</p><p><span style="color:red">$result = JoinText($p1, $p2, $p3)
</span></p><p>write-host $result
</p><p>
 </p><p><strong>script2-right.ps1
</strong></p><p>$p1 = "some text 1"
</p><p>$p2 = "some text 2"
</p><p>$p3 = "some text 3"
</p><p><span style="color:#00b050">$result = JoinText -p1 $p1 -p2 $p2 -p3 $p3
</span></p><p>write-host $result
</p>