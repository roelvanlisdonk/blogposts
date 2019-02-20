---
ID: 1849
post_title: >
  Overwriting the msiexec property
  TARGETDIR for x86 and x64 application
  setups
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/12/23/overwriting-the-msiexec-property-targetdir-for-x86-and-x64-application-setups/
published: true
post_date: 2010-12-23 15:37:46
---
<p>If you want to remove a application from you’re system you can use:</p>  <p>   <br />msiexec /x {product_guid}    <br />like: msiexec /x {2EAB2958-5675-4773-9BF6-2C8FB9DF9CC6}</p>  <p>&#160;</p>  <p>If you want to install a *.msi package, but want don’t want to install the application to the default installation folder you can overwrite the TARGETDIR property, like   <br /></p>  <p>msiexec /i &quot;C:\Temp\MyFirstApp.msi&quot; TARGETDIR=&quot;D:\Programs\MyFirstApp&quot;   <br /></p>  <p>But if you’re msi package is created with Microsoft Visual Studio and the property Targetplatform of the setup project is set to x86, you can’t overwrite the TARGETDIR to Program Files, when you execute the following line on a x64 machine:</p> msiexec /i &quot;C:\Temp\MyFirstApp.msi&quot; TARGETDIR=&quot;C:\Program Files&quot;  <br />  <p>&#160;</p>  <p>The msiexec will change it back to &quot;C:\Program Files (x86)&quot;</p>  <p>&#160;</p>  <p>Just so you know why the application is installed in the &quot;C:\Program Files (x86)&quot; folder instead of the &quot;C:\Program Files&quot; folder.</p>