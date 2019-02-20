---
ID: 1239
post_title: >
  TFS 2010 Best Practices and TFS
  Structure
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/16/tfs-best-practices/
published: true
post_date: 2010-04-16 08:13:43
---
<p>We used the TFS Best Practices Guide on CodePlex for deploying and using our TFS server: <a title="http://tfsguide.codeplex.com/" href="http://tfsguide.codeplex.com/">http://tfsguide.codeplex.com/</a></p>  <p>&#160;</p>  <p><img title="TeamDevGuide.gif" alt="TeamDevGuide.gif" src="http://i3.codeplex.com/Project/Download/FileDownload.aspx?ProjectName=TFSGuide&amp;DownloadId=12864" width="200" height="255" /></p>  <p>&#160;</p>  <p>Based on this guide we used the following TFS Structure:</p>  <p class="Normal8"><span style="color: black; font-size: 11.5pt" lang="EN-US">     <p>&#160;</p>   </span></p>  <p class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">$MyTeamProject1      <p></p>   </span></p>  <p style="text-indent: 36pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/Main <span style="mso-tab-count: 6">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Can contain solution (.sln) files      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 36pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/Source      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 72pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/MyApp1 <span style="mso-tab-count: 2">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span><span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains MyApp1.sln file      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 108pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/ClassLibrary1 <span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160; </span><span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains ClassLibrary1.csproj      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 108pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/MyApp1Web <span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160; </span><span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains Default.aspx      <p></p>   </span></p>  <p style="margin-left: 144pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/ClassLibrary1Tests <span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains test project and code      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 108pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/MyApp1WebTests <span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains test project and code      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 72pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/MyApp2 <span style="mso-tab-count: 3">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains MyApp2.sln file      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 108pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/ClassLibrary2 <span style="mso-tab-count: 2">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains ClassLibrary1.csproj      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 108pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/MyApp2Web <span style="mso-tab-count: 2">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains Default.aspx      <p></p>   </span></p>  <p style="margin-left: 144pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/ClassLibrary2Tests <span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains test project and code      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 108pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/MyApp2WebTests <span style="mso-tab-count: 1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains test project and code      <p></p>   </span></p>  <p style="margin-left: 108pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/SharedBinaries <span style="mso-tab-count: 3">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Shared binaries e.g. libraries      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 72pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/SharedSource <span style="mso-tab-count: 3">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Shared source code      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 36pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/Docs <span style="mso-tab-count: 5">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Contains product documentation      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 36pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/Tests <span style="mso-tab-count: 5">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; color: black; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="color: black; font-size: 9pt" lang="EN-US">Container for tests      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 72pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/FunctionalTests      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 72pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/PerformanceTests      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 72pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/SecurityTests      <p></p>   </span></p>  <p style="text-indent: 36pt" class="Default"><span style="font-size: 9pt" lang="EN-US">/TeamBuildTypes <span style="mso-tab-count: 5">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </span></span><span style="font-family: wingdings; font-size: 9pt; mso-ascii-font-family: &#39;Times New Roman&#39;; mso-hansi-font-family: &#39;Times New Roman&#39;; mso-char-type: symbol; mso-symbol-font-family: wingdings" lang="EN-US"><span style="mso-char-type: symbol; mso-symbol-font-family: wingdings">à</span></span><span style="font-family: wingdings; font-size: 9pt; mso-bidi-font-family: wingdings" lang="EN-US"> </span><span style="font-size: 9pt" lang="EN-US">Created automatically by Team Build.      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 36pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/BuildType1      <p></p>   </span></p>  <p style="text-indent: 36pt; margin-left: 36pt" class="Normal8"><span style="color: black; font-size: 9pt" lang="EN-US">/BuildType2      <p></p>   </span></p>  <p class="Default"><span lang="EN-US">     <p>&#160;</p>   </span></p>