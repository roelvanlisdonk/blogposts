---
ID: 591
post_title: 'Best Practices C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/08/03/best-practices-c-2/
published: true
post_date: 2009-08-03 09:33:35
---
<p>This article will be updated every time I run into a best practice.</p>  <p><strong>Checklist Microsoft Visual Studio 2008 Solution and Projects      <br /></strong>- Solution name should be Customer.Product.sln, like MyCustomer.MyProduct.sln     <br />- Project name should be Customer.Product.Subsystem.csproj, like MyCustomer.MyProduct.MySubsystem.csproj     <br />- Setup project name should be Customer.Product.Subsystem.Setup.csproj, like MyCustomer.MyProduct.MySubsystem.Setup.csproj     <br />- Test project name should be Customer.Product.Test.csproj, like MyCustomer.MyProduct.Test.csproj     <br />- Create 1 C# project per subsystem and 1 folder per layer, like BC, BE, Dac, Common etc.     <br />- Create 1 Setup project per subsystem     <br />- Create 1 Test C# project per solution and 1 folder per subsystem in the test C# project     <br />- For each project check the .NET version you want to build against (Target Platform)     <br />- Enable “Check for arithmetic overflow/underflow” on debug build     <br />- Disable “Check for arithmetic overflow/underflow” on release build</p>  <p><strong>Checklist C# Projects</strong>     <br />- Use String.Format to concatenate strings &lt; 5     <br />- Use StringBuilder to concatenate strings &gt;=5     <br />- Never use relative paths, because if an executable is called by an other executable or batch file located in an other folder the working directory is not the location of the executable.     <br />&#160; Always use</p>  <pre class="code"><span style="color: blue">        public string </span>AssemblyDirectory
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">string </span>codeBase = <span style="color: #2b91af">Assembly</span>.GetExecutingAssembly().CodeBase;
                <span style="color: #2b91af">UriBuilder </span>uri = <span style="color: blue">new </span><span style="color: #2b91af">UriBuilder</span>(codeBase);
                <span style="color: blue">string </span>path = <span style="color: #2b91af">Uri</span>.UnescapeDataString(uri.Path);
                <span style="color: blue">return </span><span style="color: #2b91af">Path</span>.GetDirectoryName(path);
            }
        }</pre>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p>Or as property</p>

<pre class="code"><span style="color: blue">        private static string </span>_assemblyDirectory = <span style="color: blue">null</span>;
        <span style="color: blue">public static string </span>AssemblyDirectory
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if</span>(_assemblyDirectory == <span style="color: blue">null</span>)
                {
                    <span style="color: blue">var </span>codeBase = <span style="color: #2b91af">Assembly</span>.GetExecutingAssembly().CodeBase;
                    <span style="color: blue">var </span>uri = <span style="color: blue">new </span><span style="color: #2b91af">UriBuilder</span>(codeBase);
                    <span style="color: blue">var </span>path = <span style="color: #2b91af">Uri</span>.UnescapeDataString(uri.Path);
                    _assemblyDirectory = <span style="color: #2b91af">Path</span>.GetDirectoryName(path);
                }

                <span style="color: blue">return </span>_assemblyDirectory;
            }
        }</pre>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p>For difference Assembly.CodeBase en Assembly.Location, see msdn</p>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p><strong>Checklist Setup Projects</strong></p>

<p>- Before editing anything on a setup project, check out the setup project by hand</p>

<p>- Change Author</p>

<p>- Change Description</p>

<p>- Change DetectNewerInstalledVersion to True</p>

<p>- Change InstallAllUsers to True</p>

<p>- Change Manufacturer</p>

<p>- Change ManufacturerUrl</p>

<p>- Change ProductName</p>

<p>- Change RemovePreviousVersions to True</p>

<p>- Change Subject</p>

<p>- Change SupportPhone</p>

<p>- Change SupportUrl</p>

<p>- Change Title</p>

<p>- Change Version</p>

<p>- Change Application Folder to “[ProgramFilesFolder][Manufacturer]\<strong>ProductName</strong>\[ProductName]”</p>

<p>- If you want to change the for “AddRemoveProgramsIcon” icon of the setup project:</p>

<p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &gt; Add a icon file to the primary output C# project</p>

<p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &gt; Open the C# project properties “Application” page</p>

<p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &gt; Select the icon file in the “Icon and manifest” dropdownbox</p>

<p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &gt; In the setup property grid select browse… &gt; click on browse in icon dialog &gt; select “All Files (*.*)” on the “Files of type” dropdownbox primairy &gt; select primary output from “you’re C# project” as source for “AddRemoveProgramsIcon”</p>

<p>Don’t use a icon selected directly from filesystem, because you can get sourcecontrol binding problems for you’re setup project, unless it is added to the project it self in the same directory as de setup project file.</p>

<p><strong>Switch</strong></p>

<p>Every switch statement should have it's own function.</p>

<p><strong>Functions</strong></p>

<p>In most cases a method should be on the object whose data it uses.</p>

<p><strong>Unittest</strong></p>

<p>Every class should have it’s own unittest class.</p>

<p>Every method should have at least one unittest (happy path)</p>

<p>Unittesttemplate:</p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>NUnit.Framework;
<span style="color: blue">using </span>NUnit.Framework.SyntaxHelpers;

<span style="color: blue">namespace </span>Customer1.Product1.Test.Subsystem1.Bc<br />{
    [<span style="color: #2b91af">TestFixture</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">DateTimeTester
    </span>{
        [<span style="color: #2b91af">TestFixtureSetUp</span>]
        <span style="color: blue">public void </span>FixtureSetUp() { <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: #a31515">&quot;This code is executed before the first test in this class is executed&quot;</span>); }
        [<span style="color: #2b91af">TestFixtureTearDown</span>]
        <span style="color: blue">public void </span>FixtureTeardown() { <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: #a31515">&quot;This code is executed after the last test in this class is executed&quot;</span>); }
        [<span style="color: #2b91af">SetUp</span>]
        <span style="color: blue">public void </span>Setup() { <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: #a31515">&quot;This code is executed before the start of every test in this class&quot;</span>); }
        [<span style="color: #2b91af">TearDown</span>]
        <span style="color: blue">public void </span>Teardown() { <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: #a31515">&quot;This code is executed after the end of every test in this class&quot;</span>); }
        [<span style="color: #2b91af">Test</span>]
        <span style="color: blue">public void </span>AddDays_HappyPath_AddedOneDayToDateTime()
        {
            <span style="color: green">// Arrange
            </span><span style="color: #2b91af">DateTime </span>currentDateTime = <span style="color: blue">new </span><span style="color: #2b91af">DateTime</span>(2009,7,1);
            <span style="color: #2b91af">DateTime </span>expectedDateTime = <span style="color: blue">new </span><span style="color: #2b91af">DateTime</span>(2009, 7, 2);

            <span style="color: green">// Act
            </span><span style="color: #2b91af">DateTime </span>addedDateTime = currentDateTime.AddDays(1);

            <span style="color: green">// Assert
            </span><span style="color: #2b91af">Assert</span>.That(addedDateTime, <span style="color: #2b91af">Is</span>.EqualTo(expectedDateTime));
        }
    }
}</pre>

<p><strong>100% Coverage, even with read-only properties</strong></p>

<p>If you have to write a unit test for properties that are read-only, like the&#160; System.Configuration.<span style="color: #2b91af">ConfigurationManager</span>.ConnectionStrings[<span style="color: #a31515">&quot;Database1&quot;</span>]&#160; <br />you can create a method with the read-only property as parameter. By doing that, you can have 100% coverage.</p>

<pre class="code"><span style="color: green">// Get connectionstring from App.config
</span><span style="color: blue">string </span>connectionString = GetConnectionString(<span style="color: #2b91af">ConfigurationManager</span>.ConnectionStrings[<span style="color: #a31515">&quot;Database1&quot;</span>])</pre>

<p><a href="http://11011.net/software/vspaste"></a></p>

<pre class="code"><span style="color: blue">public static string </span>GetConnectionString(<span style="color: #2b91af">ConnectionStringSettings </span>section)
       {
           <span style="color: blue">if </span>(section == <span style="color: blue">null</span>)
           {
               <span style="color: blue">throw new </span><span style="color: #2b91af">NullReferenceException</span>(<span style="color: #a31515">@&quot;No xmlnode &lt;configuration&gt;...&lt;connectionStrings&gt;&lt;add name=&quot;&quot;Database1&quot;&quot;... in App.config&quot;</span>);
           }
           <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(section.ConnectionString))
           {
               <span style="color: blue">throw new </span><span style="color: #2b91af">NullReferenceException</span>(<span style="color: #a31515">@&quot;Xmlnode attribute &lt;configuration&gt;...&lt;connectionStrings&gt;&lt;add name=&quot;&quot;Database1&quot;&quot; connectionString=&quot;&quot;... was empty&quot;</span>);
           }
           <span style="color: blue">return </span><span style="color: #2b91af">ConfigurationManager</span>.ConnectionStrings[<span style="color: #a31515">&quot;Database1&quot;</span>].ConnectionString;
       }</pre>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p><strong>Logging</strong></p>

<p>If you want to log all the items in an string array, you can use the string.Join function:</p>

<p><span style="color: blue">string</span>[] args = {<span style="color: #a31515">&quot;item1&quot;</span>, <span style="color: #a31515">&quot;item2&quot;</span>, <span style="color: #a31515">&quot;item3&quot;</span>};</p>

<p><span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Join(<span style="color: #a31515">&quot;,&quot;</span>,args));</p>

<p><strong>Global Exception Handling in ASP .NET</strong></p>

<p>As a good programmer, you normally want to catch all exceptions at the highest tier in code so that your program has the chance to display the error message to the user or log it to the appropriate location. Under ASP.NET, you can do so easily by overriding the Application_Error event in Global.asax file.</p>

<pre class="code"><span style="color: blue">protected void </span>Application_Error(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
{
    <span style="color: #2b91af">Exception </span>ex = Server.GetLastError();

    <span style="color: green">// Perform error logging here...

    // Clear the error and maybe redirect to some other page...
    </span>Server.ClearError();
}</pre>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p><a href="http://11011.net/software/vspaste"></a><strong>Global Exception Handling in a .NET console application or Windows Service</strong></p>

<p>Unfortunately, there is no concept of Global.asax in a winform or console application in .NET. In a windows form application, the equivalent global catch all is available by listening to the ThreadException and AppDomain UnhandledException events.</p>

<pre class="code"><span style="color: blue">class </span><span style="color: #2b91af">Program
    </span>{
        [<span style="color: #2b91af">STAThread</span>]
        <span style="color: blue">static void </span>Main()
        {
            <span style="color: green">// Catch all unhandled exceptions in all threads.
            </span><span style="color: #2b91af">AppDomain</span>.CurrentDomain.UnhandledException += UnhandledExceptionHandler;
        }
        <span style="color: blue">private static void </span>UnhandledExceptionHandler(<span style="color: blue">object </span>sender, <span style="color: #2b91af">UnhandledExceptionEventArgs </span>args)
        {
            <span style="color: blue">try
            </span>{
                <span style="color: green">// Log error here or prompt user...
            </span>}
            <span style="color: blue">catch </span>{ }
        }
    }</pre>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p><strong>Global Exception Handling in a .NET windows application</strong></p>

<pre class="code"><span style="color: blue">class </span><span style="color: #2b91af">Program
    </span>{
        [<span style="color: #2b91af">STAThread</span>]
        <span style="color: blue">static void </span>Main()
        {
            <span style="color: green">// Catch all unhandled exceptions
            </span>System.Windows.Forms.<span style="color: #2b91af">Application</span>.ThreadException += ThreadExceptionHandler;

            <span style="color: green">// Catch all unhandled exceptions in all threads.
            </span><span style="color: #2b91af">AppDomain</span>.CurrentDomain.UnhandledException += UnhandledExceptionHandler;

            System.Windows.Forms.<span style="color: #2b91af">Application</span>.Run(<span style="color: blue">new </span><span style="color: #2b91af">MainForm</span>());
        }
        <span style="color: blue">private static void </span>ThreadExceptionHandler(<span style="color: blue">object </span>sender, System.Threading.<span style="color: #2b91af">ThreadExceptionEventArgs </span>args)
        {
            <span style="color: blue">try
            </span>{
                <span style="color: green">// Log error here or prompt user...
            </span>}
            <span style="color: blue">catch </span>{ }
        }
        <span style="color: blue">private static void </span>UnhandledExceptionHandler(<span style="color: blue">object </span>sender, <span style="color: #2b91af">UnhandledExceptionEventArgs </span>args)
        {
            <span style="color: blue">try
            </span>{
                <span style="color: green">// Log error here or prompt user...
            </span>}
            <span style="color: blue">catch </span>{ }
        }
    }</pre>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p>Information found at <a title="http://www.cubiczone.com/Articles/tabid/65/EntryID/24/Default.aspx" href="http://www.cubiczone.com/Articles/tabid/65/EntryID/24/Default.aspx">http://www.cubiczone.com/Articles/tabid/65/EntryID/24/Default.aspx</a></p>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p><strong>TypeOf</strong></p>

<p>If you need to get the metadata of a type, use the typeof C# operator:</p>

<p>Console.WriteLine(typeof(string).FullName);</p>

<p><strong>Chaining Constructors</strong></p>

<p>Using chaining constructors if you define multiple constructors that use the (partial) same logic.</p>

<p><strong>Constant and Read-Only fields</strong></p>

<p>Use constant fields for fields that contain constant data that is know at compile time. Use read-only fields for fields that contain constant data that is not know at compile time and can be set in the constructor</p>

<p><strong>The Is keyword</strong></p>

<p>Use the Is keyword to check for correct type</p>

<p><strong>Use thow; to rethrow an exception</strong></p>

<p>This will preserve the original context of the exceptioin</p>

<p><strong>Default</strong></p>

<p>Use the default keyword to get the default value for a type even generic types:</p>

<pre class="code"><span style="color: blue">var </span>result = <span style="color: blue">default</span>(T);</pre>

<p><strong>Garbage Collection</strong></p>

<p>Don’t call the garbage collection from code, but if you have to (because you are managing a very large array or something), call garbage collection as follow:</p>

<p>GC.Collect();
  <br />

  <br />GC.WaitForPendingFinalizers();</p>

<p>Never use destructors or finalize methods, unless you have to, because you are using unmanaged code, because declaring destructors or finalize methods marks the object as finalizable and stores a pointer on the finalization que and then there is a whole story to tell,&#160; but the point is, it is slower.</p>

<p><a href="http://11011.net/software/vspaste"></a></p>