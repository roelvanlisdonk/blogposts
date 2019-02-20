---
ID: 5260
post_title: >
  Calling a function from another
  PowerShell script file in the same
  folder with “relative path”
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/10/05/calling-a-function-from-another-powershell-script-file-in-the-same-folder-with-relative-path/
published: true
post_date: 2018-10-05 14:38:53
---
<p>
 </p><p>If you want to execute a function from another PowerShell script file, you can "dot-source" the file.
</p><p>The "." is a special operator in PowerShell that can load another PowerShell script file en import all code in it.
</p><p>
 </p><p>Assume both PowerShell scripts are in the same folder, we can use the code in script1.ps1 in script2.ps1 in the following way: 
</p><p>
 </p><p><strong>PowerShell script1.ps1
</strong></p><p>
 </p><p>function ReturnGivenText {
</p><p>Param(
</p><p>                [Parameter(Mandatory=$True)]
</p><p>        [string]$text
</p><p>    )
</p><p>    return $text
</p><p>}
</p><p>
 </p><p><strong>PowerShell script2.ps1
</strong></p><p>$text = ReturnGivenText -text "Hello world"
</p><p>write-host $text
</p><p>
 </p><p>This will output:
</p><p>Hello world
</p><p>
 </p><p>Note: I use the PowerShell &gt;3 global variable $PSScriptRoot, to make the relative path, absolute, so we can use the "." operator.
</p><p>
 </p>