---
ID: 474
post_title: 'ASP .NET Could not find a part of the path &#039;c:\windows\system32\inetsrv&#8230;&#8230;&#039;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/asp-net-could-not-find-a-part-of-the-path-cwindowssystem32inetsrv/
published: true
post_date: 2009-05-25 12:56:52
---
<p></p>  <div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClass0A7E3E5449EA47D580A19C69866D4790">         <p>When you want to read a file in you're website folder, you get the error:           <br />Exception Details: System.IO.DirectoryNotFoundException: Could not find a part of the path 'c:\windows\system32\inetsrv.........'.            <br />            <br />This is because you will have to map you're path: <a title="http://msdn.microsoft.com/en-us/library/ms178116.aspx" href="http://msdn.microsoft.com/en-us/library/ms178116.aspx">http://msdn.microsoft.com/en-us/library/ms178116.aspx</a>            <br /></p>          <pre class="code"><span style="color: #2b91af"> DataSet </span>ds = <span style="color: blue">new </span><span style="color: #2b91af">DataSet</span>();
 ds.ReadXml(Server.MapPath(<span style="color: #a31515">@&quot;~\Data\ImageInGridView.xml&quot;</span>));</pre>
        <a href="http://11011.net/software/vspaste"></a>

        <p>
          <br /><strong>StackTrace info</strong>

          <br />[DirectoryNotFoundException: Could not find a part of the path 'c:\windows\system32\inetsrv\Data\ImageInGridView.xml'.] System.IO.__Error.WinIOError(Int32 errorCode, String maybeFullPath) +492 System.IO.FileStream.Init(String path, FileMode mode, FileAccess access, Int32 rights, Boolean useRights, FileShare share, Int32 bufferSize, FileOptions options, SECURITY_ATTRIBUTES secAttrs, String msgPath, Boolean bFromProxy) +1038 System.IO.FileStream..ctor(String path, FileMode mode, FileAccess access, FileShare share, Int32 bufferSize) +113 System.Xml.XmlDownloadManager.GetStream(Uri uri, ICredentials credentials) +78 System.Xml.XmlUrlResolver.GetEntity(Uri absoluteUri, String role, Type ofObjectToReturn) +51 System.Xml.XmlTextReaderImpl.OpenUrlDelegate(Object xmlResolver) +44 System.Threading.CompressedStack.runTryCode(Object userData) +54 System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup(TryCode code, CleanupCode backoutCode, Object userData) +0 System.Threading.CompressedStack.Run(CompressedStack compressedStack, ContextCallback callback, Object state) +174 System.Xml.XmlTextReaderImpl.OpenUrl() +199 System.Xml.XmlTextReaderImpl.Read() +53 System.Xml.XmlTextReader.Read() +12 System.Xml.XmlReader.MoveToContent() +70 System.Data.DataSet.ReadXml(XmlReader reader, Boolean denyResolving) +254 System.Data.DataSet.ReadXml(String fileName) +62 </p>
      </div>
    </div>
  </div>
</div>