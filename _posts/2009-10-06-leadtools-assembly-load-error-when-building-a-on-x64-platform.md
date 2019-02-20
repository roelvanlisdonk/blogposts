---
ID: 738
post_title: >
  Leadtools assembly load error, when
  building on a x64 platform
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/06/leadtools-assembly-load-error-when-building-a-on-x64-platform/
published: true
post_date: 2009-10-06 11:40:32
---
<p>When you use leadtools in an assemlby and reference this assemlby by another assembly (e.g. a dll uses the Leadtools.Forms.Ocr and an executable references that dll), make sure that both assemlbies reference the Leadtools assembly, if not referenced assemlby load errors can occur.   <br />    <br />When building these assemblies on an x64 platform and you are using the x86 leadtools assemblies, make sure you’re assemblies are build targeting the x86 platform, else assembly load errors can occur.&#160; <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image3.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image_thumb3.png" width="636" height="219" /></a>     <br />    <br /><strong>Erros</strong>    <br />Could not load file or assembly 'Leadtools, Version=16.0.0.0, Culture=neutral, PublicKeyToken=9cf889f53ea9b907' or one of its dependencies. An attempt was made to load a program with an incorrect format.    <br />or    <br />Could not load file or assembly 'Leadtools.Barcode, Version=16.0.0.0, Culture=neutral, PublicKeyToken=9cf889f53ea9b907'    <br />or    <br />Could not load file or assembly 'Leadtools.Codecs, Version=16.0.0.0, Culture=neutral, PublicKeyToken=9cf889f53ea9b907'    <br />or    <br />Could not load file or assembly 'Leadtools.Forms, Version=16.0.0.0, Culture=neutral, PublicKeyToken=9cf889f53ea9b907'    <br />or    <br />Could not load file or assembly 'Leadtools.Forms.Ocr, Version=16.0.0.0, Culture=neutral, PublicKeyToken=9cf889f53ea9b907'    <br />or    <br />Could not load file or assembly 'Leadtools.Forms.Ocr.Plus, Version=16.0.0.0, Culture=neutral, PublicKeyToken=9cf889f53ea9b907'    <br />etc.    </p>