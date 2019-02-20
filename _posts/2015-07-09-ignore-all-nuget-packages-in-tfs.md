---
ID: 4473
post_title: Ignore all NuGet packages in TFS
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/07/09/ignore-all-nuget-packages-in-tfs/
published: true
post_date: 2015-07-09 09:24:49
---
<p>I didn’t want to add the NuGet packages of my Visual Studio solution to TFS, because I download all NuGet packages during build. </p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image21.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image_thumb21.png" width="580" height="522" /></a></p>  <p>&#160;</p>  <p>To exclude all NuGet packages from TFS:</p>  <ul>   <li>Add a <strong>folder</strong> “.nuget” to the folder that also contains the “packages” folder and in most cases the “solution file”.</li>    <ul>     <li>add a file to the “.nuget” folder with the name “NuGet.config”</li>      <ul>       <li>contents of the file:</li>        <p>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;         <br />&lt;configuration&gt;          <br />&#160; &lt;solution&gt;          <br />&#160;&#160;&#160; &lt;add key=&quot;disableSourceControlIntegration&quot; value=&quot;true&quot; /&gt;          <br />&#160; &lt;/solution&gt;          <br />&lt;/configuration&gt;</p>     </ul>   </ul>    <li>Add a <strong>file</strong> “.tfignore”&#160; to the folder that also contains the “packages” folder and in most cases the “solution file”.</li>    <ul>     <li>contents of the file:</li>      <ul>       <li>\packages</li>     </ul>   </ul> </ul>  <p>&#160;</p>  <p>More information: <a title="http://stackoverflow.com/questions/26604506/tfs-vs-2013-ignore-all-nuget-packages" href="http://stackoverflow.com/questions/26604506/tfs-vs-2013-ignore-all-nuget-packages">http://stackoverflow.com/questions/26604506/tfs-vs-2013-ignore-all-nuget-packages</a></p>