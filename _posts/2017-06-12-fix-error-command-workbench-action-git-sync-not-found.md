---
ID: 5085
post_title: 'Fix error: command &lsquo;workbench.action.git.sync&rsquo; not found'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/06/12/fix-error-command-workbench-action-git-sync-not-found/
published: true
post_date: 2017-06-12 10:01:55
---
In a previous visual studio code version I created a custom keybinding:

{ "key": "ctrl+shift+s", "command": "workbench.action.git.sync" }

In the current version of visual studio code I got the error:

Warn: command ‘workbench.action.git.sync’ not found.

<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2017/06/image.png" rel="lightbox"><img style="margin: 0px; display: inline; background-image: none;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2017/06/image_thumb.png" alt="image" width="703" height="100" border="0" /></a>

Changing the command to ‘git.sync’ fixed the error.