---
ID: 679
post_title: 'Install (create), Uninstall (delete) a C# Windows Service on the command line with sc.exe or with C# code'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/03/install-create-uninstall-delete-a-c-windows-service-on-the-command-line-with-sc-exe/
published: true
post_date: 2009-09-03 12:53:12
---
<p>To install a C# Windows Service without running the ProjectInstaller class in the C# service, use sc.exe.    <br />    <br />For example     <br /><strong>sc create MyService start= auto binPath= &quot;C:\Program Files (x86)\MyCustomer\MyService\MyService.exe&quot; DisplayName= MyService</strong>     <br />    <br />Remember, a space is required between the equal sign and the value for the optional parameters.     <br />See <a title="http://support.microsoft.com/kb/251192/en-us" href="http://support.microsoft.com/kb/251192/en-us">http://support.microsoft.com/kb/251192/en-us</a></p>  <p>You can delete a service with sc.exe.    <br />Before you use sc.exe to delete a service, make sure that all instances of the mmc plug-in “<strong>services.msc</strong>” are closed and there are no running instances of the service.     <br />Use Process Explorer.exe (<a title="http://technet.microsoft.com/en-us/sysinternals/bb795533.aspx" href="http://technet.microsoft.com/en-us/sysinternals/bb795533.aspx">http://technet.microsoft.com/en-us/sysinternals/bb795533.aspx</a>) to kill all running instances of the service.     <br />If you don’t, sc delete will give a “Service is marked for deletion” error. This error disappears by rebooting the server or closing the services.msc and closing all running instances of the service.     <br />    <br />For example:     <br /><strong>sc delete MyService      <br /></strong>    <br />By default Windows 2000 Professional does not have the sc.exe, you can download it from <u><a href="http://www.dynawell.com/download/reskit/microsoft/win2000/sc.zip">http://www.dynawell.com/download/reskit/microsoft/win2000/sc.zip</a>       <br /></u>    <br />If you want to execute sc.exe from C# code, you could use a function like:</p>  <pre class="code"><span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Create a Windows service when it does not exist, else configure it.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;name&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;displayName&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;binPath&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;userName&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;unecryptedPassword&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;startupType&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">public void </span>Configure(<span style="color: blue">string </span>name, <span style="color: blue">string </span>displayName, <span style="color: blue">string </span>binPath, <span style="color: blue">string </span>userName, <span style="color: blue">string </span>unecryptedPassword, <span style="color: blue">string </span>startupType)
        {

            <span style="color: green">// Determine statuptype
            </span><span style="color: blue">string </span>startupTypeConverted = <span style="color: blue">string</span>.Empty;
            <span style="color: blue">switch </span>(startupType)
            {
                <span style="color: blue">case </span><span style="color: #a31515">&quot;Automatic&quot;</span>:
                    startupTypeConverted = <span style="color: #a31515">&quot;auto&quot;</span>;
                    <span style="color: blue">break</span>;
                <span style="color: blue">case </span><span style="color: #a31515">&quot;Disabled&quot;</span>:
                    startupTypeConverted = <span style="color: #a31515">&quot;disabled&quot;</span>;
                    <span style="color: blue">break</span>;
                <span style="color: blue">case </span><span style="color: #a31515">&quot;Manual&quot;</span>:
                    startupTypeConverted = <span style="color: #a31515">&quot;demand&quot;</span>;
                    <span style="color: blue">break</span>;
                <span style="color: blue">default</span>:
                    startupTypeConverted = <span style="color: #a31515">&quot;auto&quot;</span>;
                    <span style="color: blue">break</span>;
            }

            <span style="color: green">// Determine if service has to be created (Create) or edited (Config)
            </span><span style="color: #2b91af">StringBuilder </span>builder = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>();
            <span style="color: blue">if </span>(<span style="color: blue">this</span>.Exists(name))
            {
                builder.AppendFormat(<span style="color: #a31515">&quot;{0} {1} &quot;</span>, <span style="color: #a31515">&quot;Config&quot;</span>, name);
            }
            <span style="color: blue">else
            </span>{
                builder.AppendFormat(<span style="color: #a31515">&quot;{0} {1} &quot;</span>, <span style="color: #a31515">&quot;Create&quot;</span>, name);
            }

            builder.AppendFormat(<span style="color: #a31515">&quot;binPath= \&quot;{0}\&quot;  &quot;</span>, binPath);
            builder.AppendFormat(<span style="color: #a31515">&quot;displayName= \&quot;{0}\&quot;  &quot;</span>, displayName);

            <span style="color: green">// Only add &quot;obj&quot; when username is not empty. If omitted the &quot;Local System&quot; account will be used
            </span><span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(userName))
            {
                builder.AppendFormat(<span style="color: #a31515">&quot;obj= \&quot;{0}\&quot;  &quot;</span>, userName);
            }

            <span style="color: green">// Only add password when unecryptedPassword it is not empty and user name is not &quot;NT AUTHORITY\Local Service&quot; or NT AUTHORITY\NetworkService
            </span><span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(unecryptedPassword) &amp;&amp; !unecryptedPassword.Equals(<span style="color: #a31515">@&quot;NT AUTHORITY\Local Service&quot;</span>) &amp;&amp; !unecryptedPassword.Equals(<span style="color: #a31515">@&quot;NT AUTHORITY\NetworkService&quot;</span>))
            {
                builder.AppendFormat(<span style="color: #a31515">&quot;password= \&quot;{0}\&quot;  &quot;</span>, unecryptedPassword);
            }

            builder.AppendFormat(<span style="color: #a31515">&quot;start= \&quot;{0}\&quot;  &quot;</span>, startupTypeConverted);

            <span style="color: green">// Execute sc.exe commando
            </span><span style="color: blue">using </span>(<span style="color: #2b91af">Process </span>process = <span style="color: blue">new </span><span style="color: #2b91af">Process</span>())
            {
                process.StartInfo.FileName = <span style="color: #a31515">@&quot;sc.exe&quot;</span>;
                process.StartInfo.Arguments = builder.ToString();
                process.StartInfo.CreateNoWindow = <span style="color: blue">true</span>;
                process.StartInfo.WindowStyle = <span style="color: #2b91af">ProcessWindowStyle</span>.Hidden;
                process.Start();
            }

        }</pre>
<a href="http://11011.net/software/vspaste"></a>