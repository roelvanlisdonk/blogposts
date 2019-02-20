---
ID: 4638
post_title: 'Microsoft ASP.NET and Web Tools 2015 (Beta8) &ndash; Visual Studio 2015'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/10/19/microsoft-asp-net-and-web-tools-2015-beta8-visual-studio-2015/
published: true
post_date: 2015-10-19 19:48:04
---
<p>Just a reminder beta 8 for ASP .NET is out:</p>  <p><a href="http://www.microsoft.com/en-us/download/confirmation.aspx?id=49442">http://www.microsoft.com/en-us/download/confirmation.aspx?id=49442</a></p>  <p>&#160;</p>  <p>If you don’t install this tooling, you will get an error (see below), when manual upgrading from beta 5 to 8 in the project.json file.</p>  <p>Don’t forget to set the Solution DNX SDK version of your project to 1.0.0-beta8.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/10/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/10/image_thumb.png" width="580" height="150" /></a></p>  <p>&#160;</p>  <p>Also make sure you set the default document, when using only static files and target the .NET Core runtime.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/10/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/10/image_thumb1.png" width="580" height="285" /></a></p>  <p>&#160;</p>  <p>&#160;</p>  <h3>Server Error in '/' Application.    <hr size="1" width="100%" /></h3>  <h4><i>Could not load file or assembly 'Microsoft.Dnx.Host.Clr' or one of its dependencies. The system cannot find the file specified.</i></h4> <b>Description: </b>An unhandled exception occurred during the execution of the current web request. Please review the stack trace for more information about the error and where it originated in the code.  <br /><b>Exception Details: </b>System.IO.FileNotFoundException: Could not load file or assembly 'Microsoft.Dnx.Host.Clr' or one of its dependencies. The system cannot find the file specified.  <br /><b>Source Error:</b>  <p><code>An unhandled exception was generated during the execution of the current web request. Information regarding the origin and location of the exception can be identified using the exception stack trace below.</code></p>  <p><b>Assembly Load Trace:</b> The following information can be helpful to determine why the assembly 'Microsoft.Dnx.Host.Clr' could not be loaded.</p>  <p><code></code>    <pre>=== Pre-bind state information ===
LOG: DisplayName = Microsoft.Dnx.Host.Clr
 (Partial)
WRN: Partial binding information was supplied for an assembly:
WRN: Assembly Name: Microsoft.Dnx.Host.Clr | Domain ID: 3
WRN: A partial bind occurs when only part of the assembly display name is provided.
WRN: This might result in the binder loading an incorrect assembly.
WRN: It is recommended to provide a fully specified textual identity for the assembly,
WRN: that consists of the simple name, version, culture, and public key token.
WRN: See whitepaper http://go.microsoft.com/fwlink/?LinkId=109270 for more information and common solutions to this issue.
LOG: Appbase = file:///C:/Users/roel/.dnx/runtimes/dnx-clr-win-x86.1.0.0-beta5/bin
LOG: Initial PrivatePath = NULL
Calling assembly : (Unknown).
===
LOG: This bind starts in default load context.
LOG: Configuration file C:\Program Files (x86)\IIS Express\iisexpress.exe.config does not exist.
LOG: No application configuration file found.
LOG: Using host configuration file: C:\Users\roel\Documents\IISExpress\config\aspnet.config
LOG: Using machine configuration file from C:\Windows\Microsoft.NET\Framework\v4.0.30319\config\machine.config.
LOG: Policy not being applied to reference at this time (private, custom, partial, or location-based assembly bind).
LOG: Attempting download of new URL file:///C:/Users/roel/.dnx/runtimes/dnx-clr-win-x86.1.0.0-beta5/bin/Microsoft.Dnx.Host.Clr.DLL.
LOG: Attempting download of new URL file:///C:/Users/roel/.dnx/runtimes/dnx-clr-win-x86.1.0.0-beta5/bin/Microsoft.Dnx.Host.Clr/Microsoft.Dnx.Host.Clr.DLL.
LOG: Attempting download of new URL file:///C:/Users/roel/.dnx/runtimes/dnx-clr-win-x86.1.0.0-beta5/bin/Microsoft.Dnx.Host.Clr.EXE.
LOG: Attempting download of new URL file:///C:/Users/roel/.dnx/runtimes/dnx-clr-win-x86.1.0.0-beta5/bin/Microsoft.Dnx.Host.Clr/Microsoft.Dnx.Host.Clr.EXE.</pre>
</p>

<p><b>Stack Trace:</b></p>

<p><code></code>

  <pre>[FileNotFoundException: Could not load file or assembly 'Microsoft.Dnx.Host.Clr' or one of its dependencies. The system cannot find the file specified.]

[TypeLoadException: The domain manager specified by the host could not be instantiated.]
   System.Web.HttpRuntime.HostingInit(HostingEnvironmentFlags hostingFlags, PolicyLevel policyLevel, Exception appDomainCreationException) +303

[HttpException (0x80004005): The domain manager specified by the host could not be instantiated.]
   System.Web.HttpRuntime.FirstRequestInit(HttpContext context) +9922864
   System.Web.HttpRuntime.EnsureFirstRequestInit(HttpContext context) +90
   System.Web.HttpRuntime.ProcessRequestNotificationPrivate(IIS7WorkerRequest wr, HttpContext context) +261</pre>
</p>

<hr size="1" width="100%" /><b>Version Information:</b> Microsoft .NET Framework Version:4.0.30319; ASP.NET Version:4.6.106.0