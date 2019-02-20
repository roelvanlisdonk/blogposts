---
ID: 5124
post_title: 'Git / Bitbucket &#8211; The remote end hung up unexpectedly &#8211; Early EOF &#8211; index-pack failed at exactly 1GB'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/10/12/git-bitbucket-the-remote-end-hung-up-unexpectedly-early-eof-index-pack-failed-at-exactly-1gb/
published: true
post_date: 2017-10-12 10:39:20
---
<p>
 </p><p>Suddenly my repository failed to clone:
</p><p>git clone <a href="https://lisdonr@git.zorgvandezaak.nl/scm/zvdz/pri.git">https://myuser@myurl.nl/scm/myproject/myrepo.git</a>
	</p><p>Cloning into 'myrepo'...
</p><p>remote: Counting objects: 332184, done.
</p><p>remote: Compressing objects: 100% (59662/59662), done.
</p><p>fatal: The remote end hung up unexpectedly020.57 MiB | 9.89 MiB/s
</p><p>fatal: early EOF
</p><p>fatal: index-pack failed
</p><p>
 </p><p>It failed at exactly 1GB.
</p><p>I found the fix at: <a href="https://community.atlassian.com/t5/Bitbucket-questions/My-git-clone-stops-at-1GB/qaq-p/70773">https://community.atlassian.com/t5/Bitbucket-questions/My-git-clone-stops-at-1GB/qaq-p/70773</a>
	</p><p>
 </p><p>It was caused by a limit in nginx reverse proxy, after increasing the limit to 2GB I could clone again.
</p><p>See: <a href="https://www.scalescale.com/tips/nginx/optimizing-nginx-for-serving-files-bigger-than-1gb/">https://www.scalescale.com/tips/nginx/optimizing-nginx-for-serving-files-bigger-than-1gb/</a>
	</p><p>
 </p><p>
 </p><p>
 </p><p>
 </p>