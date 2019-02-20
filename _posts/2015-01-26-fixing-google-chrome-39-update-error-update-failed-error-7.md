---
ID: 4261
post_title: 'Fixing Google Chrome 39 update error: Update failed (error: 7)'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/01/26/fixing-google-chrome-39-update-error-update-failed-error-7/
published: true
post_date: 2015-01-26 21:57:05
---
<p>When updating Google Chrome 39 64 bit on Windows 8.1 I was getting the error:</p>  <p><em>Update failed (error: 7) An error occurred while checking for updates: Google Chrome or Google Chrome Frame cannot be updated due to inconsistent Google Update Group Policy settings. Use the Group Policy Editor to set the update policy override for the Google Chrome Binaries application and try again; see http://goo.gl/uJ9gV for details.</em></p>  <p>&#160;</p>  <p>To solve this problem:</p>  <ul>   <li>Close all Google Chrome instances</li>    <li>Start &gt; Run &gt; regedit </li>    <li>Find and open HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Update\</li> </ul>  <p>If you have the following values listed under the above key then all attempts to update Google Chrome and/or Google Chrome Frame will fail:</p>  <ul>   <li>Update{8A69D345-D564-463C-AFF1-A69D9E530F96} </li>    <li>Update{8BA986DA-5100-405E-AA35-86F34A02ACBF}</li> </ul>  <p>In my case it was only: Update{8A69D345-D564-463C-AFF1-A69D9E530F96}</p>  <p>After removing this registry key and restarting Google Chrome I was able to update to Chrome 40</p>