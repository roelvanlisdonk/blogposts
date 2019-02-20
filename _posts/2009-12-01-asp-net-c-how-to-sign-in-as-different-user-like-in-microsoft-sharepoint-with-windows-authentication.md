---
ID: 825
post_title: 'ASP .NET &#8211; C# &#8211; How to &#8220;Sign in as Different User&#8221; like in Microsoft SharePoint with Windows Authentication'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/01/asp-net-c-how-to-sign-in-as-different-user-like-in-microsoft-sharepoint-with-windows-authentication/
published: true
post_date: 2009-12-01 14:05:32
---
<p>If you’re using only Windows Authentication in you’re C# ASP .NET web application, there is no build in support for the user to “log out” or to “Sign in as Different User”, like in Microsoft Office SharePoint Server:   <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image9.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb9.png" width="244" height="157" /></a>&#160; <br />    <br />The only way to make this work “cross-browser” (Tested on IE5, IE5.5, IE6, IE7, IE8, FireFox 3.5.5, Google Chrome 3.0.195.33) is to send a 401 HttpResponse to force the browser to re-authenticate it self. Well there are numerous pages describing the fact you should send a 401 HttpResponse within the ASP .NET C# web application, but few give a complete example. This post describers the complete example of sending a 401 HttpResponse to force the browser to re-authenticate it self. In this example I use a IIS server in a domain called “MyDomain”, but this can be replaced by a IIS Server in a workgroup, then you should replace “MyDomain” with the name of the server, eg. “MyIISServer”     <br /></p>  <p>- In Microsoft Visual Studio 2008, create a new web application <strong>File &gt; New &gt; Project &gt; Visual C# &gt; Web &gt; ASP .NET Web Application</strong>    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image10.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb10.png" width="507" height="367" /></a>&#160; <br />    <br />- In Microsoft Visual Studio 2008, make sure you’re website project properties are set to: “Use Local IIS Web server”. Found in menu <strong>Project &gt; MyWebSite Properties &gt; Web</strong>     <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb.png" width="571" height="181" /></a>     <br />    <br />- Click on “Create Virtual Directory” to make sure the virtual directory exists in IIS.     <br />- In the IIS 7 Manager, click on<strong> “MyWebSite” &gt; “Features View” &gt; “Authentication”</strong>     <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image1.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb1.png" width="364" height="386" /></a>     <br />    <br />- Disable “Anonymous Authentication”     <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image2.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb2.png" width="370" height="223" /></a>     <br />    <br />- Enable “Windows Authentication” (if not shown in Vista, Windows Server 2008 or Windows 7, install it via <strong>“Control Panel” &gt; “Programs and Features” &gt; “Turn Windows features on or off” &gt; &quot;Internet Information Services&quot; &gt; &quot;World Wide Web Services&quot; &gt; &quot;Security&quot; &gt; &quot;Windows Authentication&quot;</strong>)     <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image3.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb3.png" width="244" height="213" /></a>&#160; <br />    <br />- Open the Web.config of you’re website in Microsoft Visual Studio 2008 and change the authentication mode to ”Windows” and set the users to allow and deny access.</p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">system.web</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">authentication </span><span style="color: red">mode</span><span style="color: blue">=</span>&quot;<span style="color: blue">Windows</span>&quot;<span style="color: blue">/&gt;
    &lt;</span><span style="color: #a31515">identity </span><span style="color: red">impersonate</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: blue">/&gt;
    &lt;</span><span style="color: #a31515">authorization</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">allow </span><span style="color: red">users</span><span style="color: blue">=</span>&quot;<span style="color: blue">MyDomain\User1,<span style="color: blue">MyDomain\User2</span></span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">deny </span><span style="color: red">users</span><span style="color: blue">=</span>&quot;<span style="color: blue">*</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">authorization</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>You should at least deny anonymous users by adding &lt;deny users = “?” /&gt;. In this example all users are denied access, except for the users: MyDomain\User1 and MyDomain\User2.
  <br />

  <br />- In Microsoft Visual Studio 2008 add 2 pages: Default.aspx and AccessDenied.aspx

  <br />- The <strong>Default.aspx</strong> should look like:</p>

<pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Default.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;MyWebsite.Default&quot; </span><span style="background: #ffee62">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: #a31515">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;

&lt;</span><span style="color: #a31515">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot; &gt;
&lt;</span><span style="color: #a31515">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">title</span><span style="color: blue">&gt;</span>Default page<span style="color: blue">&lt;/</span><span style="color: #a31515">title</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">form </span><span style="color: red">id</span><span style="color: blue">=&quot;mainForm&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">div</span><span style="color: blue">&gt;&lt;</span><span style="color: #a31515">p</span><span style="color: blue">&gt;</span>Hello <span style="color: blue">&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;UserLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Label&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">p</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">div</span><span style="color: blue">&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;SignInAsADifferentUserLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;SignInAsADifferentUserLinkButton_Click&quot;&gt;</span>Sign in as a different user<span style="color: blue">&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">html</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>- The <strong>Default.aspx.cs</strong> should look like:</p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Web;

<span style="color: blue">namespace </span>MyWebsite
{ <br />    <span style="color: blue">public partial class </span><span style="color: #2b91af">Default </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Event fires on every page load
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: green">// Show the current logged on user
            </span>UserLabel.Text = Request.LogonUserIdentity.Name;

            <span style="color: green">// Make sure the browser does not cache this page
            </span><span style="color: blue">this</span>.DisablePageCaching();
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Event fires when user clicks on the &quot;SignInAsADifferentUserLinkButton&quot;
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">protected void </span>SignInAsADifferentUserLinkButton_Click(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: green">// Redirect to the &quot;log out&quot; page cq &quot;sign in as a different user&quot; page
            </span>Response.Redirect(<span style="color: #a31515">&quot;AccessDenied.aspx&quot;</span>);
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Make sure the browser does not cache this page
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>DisablePageCaching()
        {
            Response.Expires = 0;
            Response.Cache.SetNoStore();
            Response.AppendHeader(<span style="color: #a31515">&quot;Pragma&quot;</span>, <span style="color: #a31515">&quot;no-cache&quot;</span>);
        }
    }<br />}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>
- The <strong>AccessDenied.aspx</strong> should look like:

<pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;AccessDenied.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;MyWebsite.AccessDenied&quot; </span><span style="background: #ffee62">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: #a31515">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;

&lt;</span><span style="color: #a31515">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot; &gt;
&lt;</span><span style="color: #a31515">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">title</span><span style="color: blue">&gt;</span>Untitled Page<span style="color: blue">&lt;/</span><span style="color: #a31515">title</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">form </span><span style="color: red">id</span><span style="color: blue">=&quot;form1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">div</span><span style="color: blue">&gt;

    &lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">html</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br />- The <strong>AccessDenied.aspx.cs</strong> should look like:</p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Web;

<span style="color: blue">namespace </span>MyWebsite
{
    <span style="color: blue"></span></pre>

<pre class="code"><span style="color: blue">public partial class </span><span style="color: #2b91af">AccessDenied </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">private int </span>_authenticationAttempts = 0;
        <span style="color: blue">public int </span>AuthenticationAttempts
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}&quot;</span>, Session[<span style="color: #a31515">&quot;AuthenticationAttempts&quot;</span>])))
                {
                    <span style="color: blue">int</span>.TryParse(Session[<span style="color: #a31515">&quot;AuthenticationAttempts&quot;</span>].ToString(), <span style="color: blue">out </span>_authenticationAttempts);
                }

                <span style="color: blue">return </span>_authenticationAttempts;
            }
            <span style="color: blue">set
            </span>{
                _authenticationAttempts = <span style="color: blue">value</span>;
                Session[<span style="color: #a31515">&quot;AuthenticationAttempts&quot;</span>] = _authenticationAttempts;
            }
        }
        <span style="color: blue">private string </span>_currentUser = <span style="color: blue">string</span>.Empty;
        <span style="color: blue">public string </span>CurrentUser
        {
            <span style="color: blue">get
            </span>{
                _currentUser = Request.LogonUserIdentity.Name;
                Session[<span style="color: #a31515">&quot;CurrentUser&quot;</span>] = _currentUser;
                <span style="color: blue">return </span>_currentUser;
            }
            <span style="color: blue">set
            </span>{
                _currentUser = <span style="color: blue">value</span>;
                Session[<span style="color: #a31515">&quot;CurrentUser&quot;</span>] = _currentUser;
            }
        }
        <span style="color: blue">private string </span>_previousUser = <span style="color: blue">string</span>.Empty;
        <span style="color: blue">public string </span>PreviousUser
        {
            <span style="color: blue">get
            </span>{
                _previousUser = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}&quot;</span>, Session[<span style="color: #a31515">&quot;PreviousUser&quot;</span>]);
                <span style="color: blue">return </span>_previousUser;
            }
            <span style="color: blue">set
            </span>{
                _previousUser = <span style="color: blue">value</span>;
                Session[<span style="color: #a31515">&quot;PreviousUser&quot;</span>] = _previousUser;
            }
        }

        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">This event fires on every page load
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: green">// Make sure the browser does not cache this page
            </span><span style="color: blue">this</span>.DisablePageCaching();

            <span style="color: green">// Increase authentication attempts
            </span><span style="color: blue">this</span>.AuthenticationAttempts = <span style="color: blue">this</span>.AuthenticationAttempts + 1;


            <span style="color: blue">if </span>(<span style="color: blue">this</span>.AuthenticationAttempts == 1)
            {
                <span style="color: green">// Change previous user to current user
                </span><span style="color: blue">this</span>.PreviousUser = <span style="color: blue">this</span>.CurrentUser;

                <span style="color: green">// Send the first 401 response
                </span><span style="color: blue">this</span>.Send401();
            }
            <span style="color: blue">else
            </span>{
                <span style="color: green">// When a browser is set to &quot;automaticaly sign in with current credentials&quot;, we have to send two 401 responses to let the browser re-authenticate itself.
                // I don't know how to determine if a browser is set to &quot;automaticaly sign in with current credentials&quot;, so two 401 responses are always send when the user
                // does not switch accounts. In Micrososft Office sharepoint the user has to supply the credentials 3 times, when the user does not switch accounts,
                // so it think this is not a problem.
                </span><span style="color: blue">if </span>(<span style="color: blue">this</span>.AuthenticationAttempts == 2 &amp;&amp; <span style="color: blue">this</span>.CurrentUser.Equals(<span style="color: blue">this</span>.PreviousUser))
                {
                    <span style="color: green">// Send the second 401 response
                    </span><span style="color: blue">this</span>.Send401();
                }
                <span style="color: blue">else
                </span>{
                    <span style="color: green">// Clear the session of the current user. This will clear all sessions objects including the &quot;AuthenticationAttempts&quot;
                    </span>Session.Abandon();
                    Session.Clear();

                    <span style="color: green">// Redirect back to the main page
                    </span>Response.Redirect(<span style="color: #a31515">&quot;Default.aspx&quot;</span>);
                }
            }
        }

        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Make sure the browser does not cache this page
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>DisablePageCaching()
        {
            Response.Expires = 0;
            Response.Cache.SetNoStore();
            Response.AppendHeader(<span style="color: #a31515">&quot;Pragma&quot;</span>, <span style="color: #a31515">&quot;no-cache&quot;</span>);
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Send a 401 response
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>Send401()
        {
            <span style="color: green">// Create a 401 response, the browser will show the log-in dialogbox, asking the user to supply new credentials, <br />            // if browser is not set to &quot;automaticaly sign in with current credentials&quot;
            </span>Response.Buffer = <span style="color: blue">true</span>;
            Response.StatusCode = 401;
            Response.StatusDescription = <span style="color: #a31515">&quot;Unauthorized&quot;</span>;

            <span style="color: green">// A authentication header must be supplied. This header can be changed to Negotiate when using keberos authentication
            </span>Response.AddHeader(<span style="color: #a31515">&quot;WWW-Authenticate&quot;</span>, <span style="color: #a31515">&quot;NTLM&quot;</span>);

            <span style="color: green">// Send the 401 response
            </span>Response.End();
        }
    }<br />}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br />- Set the Default.aspx as Start Page and start debugging the website.

  <br />&#160;&#160; In IE depending on the setting <strong>Tools &gt; Options &gt; Security &gt; Local intranet &gt; Custom level... &gt; User Authentication &gt; Logon</strong>, the browser will show the windows logon dialog box.

  <br />&#160;&#160; If the site is not in the “Local Intranet Zone” you adjust the same setting on “Internet” and “Trusted Sites”&#160; <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image4.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb4.png" width="275" height="310" /></a>

  <br />

  <br />- Login to the website

  <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image5.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb5.png" width="341" height="257" /></a>

  <br />

  <br />- The website will show:

  <br />&#160;<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image6.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb6.png" width="362" height="226" /></a>

  <br />

  <br />- Click on the “Sign in as a different user”, this will show the windows dialog box

  <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image7.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb7.png" width="362" height="275" /></a>

  <br />

  <br />- The windows dialog box will always appear, but when the user supplies the same credentials as the logged in user and IE security setting for <strong>“User Authentication” &gt; “Logon”</strong> is set to “Prompt for user name and password”. The user will be asked to supply the credential 2 times.

  <br />- I think this is not a problem, because you want to sign in as a different user, so this will never occur.

  <br />

  <br />- After supplying the correct credentials the new user is logged in.

  <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image8.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb8.png" width="347" height="251" /></a>

  <br />

  <br />By looking at the MSIL code of the Microsoft.SharePoint.ApplicationPages.dll, I guess this is the way Microsoft Sharepoint does it, using the _layouts\AccessDenied.aspx

  </p>