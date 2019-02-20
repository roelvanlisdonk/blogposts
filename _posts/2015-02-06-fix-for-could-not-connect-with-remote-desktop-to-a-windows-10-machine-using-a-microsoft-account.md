---
ID: 4272
post_title: 'Fix for: Could not connect with Remote Desktop to a Windows 10 machine using a Microsoft account.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/02/06/fix-for-could-not-connect-with-remote-desktop-to-a-windows-10-machine-using-a-microsoft-account/
published: true
post_date: 2015-02-06 10:25:01
---
<p>On my home network I wanted to set up a Remote Desktop connection to a Windows 10 machine from a Windows 8.1 machine, by using the credentials of a Microsoft account. Both machines were using the same Microsoft account to login.</p>  <p>&#160;</p>  <p>Turns out I had 2 problems, first on the Windows 10 machine I had not turned on sharing.</p>  <p>When I went to Control Panel\Homegroup, on the right of the screen a text appeared to enabled sharing, when I clicked OK, I could connect with Remote Desktop to the machine, but then I had to enter credentials.</p>  <p>&#160;</p>  <p>Assuming my email address, used to login with my a Microsoft Account is: <a href="mailto:john@tools.com">john@tools.com</a> then you should enter the username as: <strong>MicrosoftAccount\john@tools.com</strong></p>  <p>&#160;</p>  <p>Yes you really have to put the text “MicrosoftAccount” in front of the email address.</p>  <p>&#160;</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/02/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/02/image_thumb1.png" width="364" height="328" /></a></p>