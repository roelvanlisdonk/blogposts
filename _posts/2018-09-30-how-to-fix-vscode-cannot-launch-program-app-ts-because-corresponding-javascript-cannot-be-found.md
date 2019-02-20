---
ID: 5251
post_title: 'How to fix: VSCode: Cannot launch program ‘…/app/ts’ because corresponding JavaScript cannot be found.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/09/30/how-to-fix-vscode-cannot-launch-program-app-ts-because-corresponding-javascript-cannot-be-found/
published: true
post_date: 2018-09-30 21:21:13
---
<p>
 </p><p>I compiled a very simple node.js express application with tsc (TypeScript) on the command line and wanted to debug it with VSCode, but when I pressed F5 I got the error: Cannot launch program '…/app/ts' because corresponding JavaScript cannot be found.
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/093018_1921_HowtofixVSC1.png" alt=""/>
	</p><p>
 </p><p>I expected the paths in the launch.json to be wrong, but that was not the case.
</p><p>The problem was that I did not generate *.js.map files.
</p><p>After I changed the tsconfig.json file, to generate *.js.map files, I could debug the application.
</p><p>
 </p><p><strong>tsconfig.json
</strong></p><p>{
</p><p>  "compileOnSave": false,
</p><p>  "compilerOptions": {
</p><p>    "target": "ES2015",   
</p><p>    "module": "commonjs",
</p><p>
		<span style="color:red">"sourceMap": true,
</span></p><p>    "strict": true
</p><p>  }
</p><p>}
</p><p>
 </p><p>
 </p>