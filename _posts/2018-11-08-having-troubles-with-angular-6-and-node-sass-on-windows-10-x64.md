---
ID: 5284
post_title: >
  Having troubles with Angular 6 and node
  sass on Windows 10 x64?
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/11/08/having-troubles-with-angular-6-and-node-sass-on-windows-10-x64/
published: true
post_date: 2018-11-08 08:33:07
---
I was getting all kinds of errors after upgrading my project to Angular 6 on Windows 10 x64, including errors on node sass.
These errors were resolved after I removed the x64 version of Node en installed the Node LTS 10.13.0 x86 (32bits) version on Windows 10 x64.

Errors ng build: Exit status 3221225477.

0 info it worked if it ends with ok

1 verbose cli [ 'C:\\Program Files\\nodejs\\node.exe',

1 verbose cli 'C:\\Program Files\\nodejs\\node_modules\\npm\\bin\\npm-cli.js',

1 verbose cli 'run',

1 verbose cli 'build' ]

2 info using npm@6.4.1

3 info using node@v10.13.0

4 verbose run-script [ 'prebuild', 'build', 'postbuild' ]

5 info lifecycle entry@0.0.0~prebuild: entry@0.0.0

6 info lifecycle entry@0.0.0~build: entry@0.0.0

7 verbose lifecycle entry@0.0.0~build: unsafe-perm in lifecycle true

8 verbose lifecycle entry@0.0.0~build: PATH: C:\Program Files\nodejs\node_modules\npm\node_modules\npm-lifecycle\node-gyp-bin;

C:\Dev\MyProject\node_modules\.bin;C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\iCLS\;C:\Program Files\Intel\Intel(R) Management Engine Components\iCLS\;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\ProgramData\chocolatey\bin;C:\Program Files\Git\cmd;C:\Program Files\dotnet\;C:\Program Files (x86)\dotnet\;C:\Program Files\Java\jdk1.8.0_181\bin;C:\Program Files\Microsoft SQL Server\130\Tools\Binn\;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files (x86)\Microsoft SQL Server\Client SDK\ODBC\130\Tools\Binn\;C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\;C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\;C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\ManagementStudio\;C:\Program Files\nodejs\;C:\Users\roelv\AppData\Local\Microsoft\WindowsApps;C:\Users\roelv\AppData\Local\Programs\Microsoft VS Code\bin;C:\Users\roelv\.dotnet\tools;C:\Users\roelv\AppData\Roaming\npm

9 verbose lifecycle entry@0.0.0~build: CWD: C:\Dev\MyProject\gateway-entry

10 silly lifecycle entry@0.0.0~build: Args: [ '/d /s /c',

10 silly lifecycle 'npm run translationsBuild &amp;&amp; npm run lint:fix &amp;&amp; ng build' ]

11 silly lifecycle entry@0.0.0~build: Returned: code: 3221225725 signal: null

12 info lifecycle entry@0.0.0~build: Failed to exec build script

13 verbose stack Error: entry@0.0.0 build: `npm run translationsBuild &amp;&amp; npm run lint:fix &amp;&amp; ng build`

13 verbose stack Exit status 3221225725

13 verbose stack at EventEmitter.&lt;anonymous&gt; (C:\Program Files\nodejs\node_modules\npm\node_modules\npm-lifecycle\index.js:301:16)

13 verbose stack at EventEmitter.emit (events.js:182:13)

13 verbose stack at ChildProcess.&lt;anonymous&gt; (C:\Program Files\nodejs\node_modules\npm\node_modules\npm-lifecycle\lib\spawn.js:55:14)

13 verbose stack at ChildProcess.emit (events.js:182:13)

13 verbose stack at maybeClose (internal/child_process.js:962:16)

13 verbose stack at Process.ChildProcess._handle.onexit (internal/child_process.js:251:5)

14 verbose pkgid entry@0.0.0

15 verbose cwd C:\Dev\MyProject

16 verbose Windows_NT 10.0.17134

17 verbose argv "C:\\Program Files\\nodejs\\node.exe" "C:\\Program Files\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "run" "build"

18 verbose node v10.13.0

19 verbose npm v6.4.1

20 error code ELIFECYCLE

21 error errno 3221225725

22 error entry@0.0.0 build: `npm run translationsBuild &amp;&amp; npm run lint:fix &amp;&amp; ng build`

22 error Exit status npm install node-sass@beta

23 error Failed at the entry@0.0.0 build script.

23 error This is probably not a problem with npm. There is likely additional logging output above.

24 verbose exit [ 3221225725, true ]