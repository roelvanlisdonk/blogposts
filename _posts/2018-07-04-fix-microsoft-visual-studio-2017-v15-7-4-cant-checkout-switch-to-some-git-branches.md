---
ID: 5218
post_title: 'Fix &#8211; Microsoft Visual Studio 2017 &#8211; v15.7.4 can&#8217;t checkout / switch to some git branches'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/07/04/fix-microsoft-visual-studio-2017-v15-7-4-cant-checkout-switch-to-some-git-branches/
published: true
post_date: 2018-07-04 09:01:13
---
I could checkout Dev, but I could not checkout master, but after some time, I could checkout the branches master, Acc and Test but not Dev.

When clicking on another branch name, Visual Studio wouldn't do anything:

<img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/07/070418_0701_FixMicrosof1.png" alt="" />

After unchecking the checkbox: "Checkout branches asynchronously when possible (Experimental)", the problem was fixed and I could checkout all branches again.

<img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/07/070418_0701_FixMicrosof2.png" alt="" />