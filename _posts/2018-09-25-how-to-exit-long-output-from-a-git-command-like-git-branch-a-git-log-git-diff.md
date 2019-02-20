---
ID: 5236
post_title: >
  How to exit long output from a git
  command (like git branch -a, git log,
  git diff)
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/09/25/how-to-exit-long-output-from-a-git-command-like-git-branch-a-git-log-git-diff/
published: true
post_date: 2018-09-25 10:33:20
---
<p>
 </p><p>When you have a lot of git branches, the output of git branch -a will be shown in the "less" program.
</p><p>The first "x" branches are shown and at the bottom the pager cursor will be shown:
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092518_0833_Howtoexitlo1.png" alt=""/>
	</p><p>
 </p><p>Now when you press "q", the less program will quit and you will be returned to the command prompt.
</p><p>Pressing "h" will show help.
</p><p>Pressing "arrow down" will scroll one row.
</p><p>Pressing "page down" will scroll a screen.
</p><p>When you reach the end of the output, the text "END" will be shown:
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/09/092518_0833_Howtoexitlo2.png" alt=""/>
	</p><p>
 </p><p>Press "q" to return to the command prompt
</p><p>
 </p><p>See: <a href="https://stackoverflow.com/questions/9483757/how-to-exit-git-log-or-git-diff">https://stackoverflow.com/questions/9483757/how-to-exit-git-log-or-git-diff</a>
	</p>