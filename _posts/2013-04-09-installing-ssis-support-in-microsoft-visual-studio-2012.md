---
ID: 3191
post_title: >
  Installing SSIS support in Microsoft
  Visual Studio 2012
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/09/installing-ssis-support-in-microsoft-visual-studio-2012/
published: true
post_date: 2013-04-09 09:53:55
---
<p>As of 5-mrt-2013, Microsoft Visual Studio 2012 supports SSIS projects by installing </p>  <p>Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</p>  <p>&#160;</p>  <p>You can download Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012 at: </p>  <p><a href="http://www.microsoft.com/en-us/download/details.aspx?id=36843">http://www.microsoft.com/en-us/download/details.aspx?id=36843</a></p>  <p>&#160;</p>  <p>On installation I got the following error:</p>  <p>SQL Server Setup could not search for updates through the Windows Update Service.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image_thumb.png" width="572" height="430" /></a></p>  <p>&#160;</p>  <p>Well I just ignored that en clicked Next.</p>  <p>&#160;</p>  <p>Than I got the error:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image_thumb1.png" width="580" height="438" /></a></p>  <p>&#160;</p>  <p>Rule &quot;Same architecture installation&quot; failed.</p>  <p>&#160;</p>  <p>The CPU architecture of installing feature(s) is different than the instance specified. To continue, add features to this instance with the same architecture.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image_thumb2.png" width="580" height="297" /></a></p>  <p>&#160;</p>  <p>This was caused by selecting &quot;Add features to an existing instance of SQL Server 2012&quot; instead of &quot;Perform a new installation of SQL Server 2012&quot;, this is the right option.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image_thumb3.png" width="580" height="438" /></a></p>  <p>&#160;</p>  <p>As mentioned on the installation page:</p>  <p><a href="http://msdn.microsoft.com/en-us/library/jj856966.aspx">http://msdn.microsoft.com/en-us/library/jj856966.aspx</a></p>  <p>On the <b>Installation Type</b> page, verify <b>Perform a new installation of SQL Server 2012</b> is selected, and then click <b>Next</b>.</p>  <p><strong>Setup will not install a new instance of SQL Server 2012 Server, but will install new SQL Server Features,</strong> including SQL Server Data Tools- Business Intelligence for Visual Studio 2012,</p>  <p>which you will select on the next Feature Selection page.</p>