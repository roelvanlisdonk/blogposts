---
ID: 5024
post_title: 'Fix: stand alone / offline update Chrome 52 to Chrome 54 doesn&rsquo;t seem to work'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/11/07/fix-stand-alone-offline-update-chrome-52-to-chrome-54-doesnt-seem-to-work/
published: true
post_date: 2016-11-07 11:31:11
---
<pre><p>I could run the offline / standalone Google Chrome 54 installer, but when I started Chrome after the installation, it was still Chrome 52, turned out Chrome 54 was added too the Program Files folder as: new_chrome, when I removed the chrome.exe and renamed the new_chrome.exe to chrome.exe the problem was resolved:</p>
</pre>

<pre><p><a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/11/image.png" rel="lightbox"><img width="818" height="394" title="image" style="display: inline; background-image: none;" alt="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/11/image_thumb.png" border="0" /></a></p>
</pre>