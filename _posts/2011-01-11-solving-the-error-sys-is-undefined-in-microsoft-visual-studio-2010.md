---
ID: 1865
post_title: 'Solving the Error: &#8216;Sys&#8217; is undefined in Microsoft Visual Studio 2010'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/11/solving-the-error-sys-is-undefined-in-microsoft-visual-studio-2010/
published: true
post_date: 2011-01-11 22:40:57
---
<p>If you create a new ASp.NET Web Application project in Microsoft Visual Studio 2010 and want to use the Sys.Debug function in an JavaScript function, you get the error ‘Sys’ is undefined. To solve this error, just drag and drop a ASP .NET scriptmanager from the toolbox on you’re master page, just below the form tag.</p>  <p>&#160;</p>  <p>Example</p>  <pre class="code"><span style="background: yellow">&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Master </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Site.master.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.Demo.TrainingWebApplication.SiteMaster&quot; </span><span style="background: yellow">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: maroon">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Strict//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd&quot;&gt;
&lt;</span><span style="color: maroon">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot; </span><span style="color: red">xml</span><span style="color: blue">:</span><span style="color: red">lang</span><span style="color: blue">=&quot;en&quot;&gt;
&lt;</span><span style="color: maroon">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">title</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">title</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;~/Styles/Site.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeadContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">body</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">form </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ScriptManager </span><span style="color: red">ID</span><span style="color: blue">=&quot;ScriptManager1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ScriptManager</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;page&quot;&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;header&quot;&gt;
            &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;title&quot;&gt;
                &lt;</span><span style="color: maroon">h1</span><span style="color: blue">&gt;
                    </span>My ASP.NET Application
                <span style="color: blue">&lt;/</span><span style="color: maroon">h1</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;loginDisplay&quot;&gt;
                &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LoginView </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeadLoginView&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">EnableViewState</span><span style="color: blue">=&quot;false&quot;&gt;
                    &lt;</span><span style="color: maroon">AnonymousTemplate</span><span style="color: blue">&gt;
                        </span>[ <span style="color: blue">&lt;</span><span style="color: maroon">a </span><span style="color: red">href</span><span style="color: blue">=&quot;~/Account/Login.aspx&quot; </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeadLoginStatus&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;</span>Log In<span style="color: blue">&lt;/</span><span style="color: maroon">a</span><span style="color: blue">&gt; </span>]
                    <span style="color: blue">&lt;/</span><span style="color: maroon">AnonymousTemplate</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">LoggedInTemplate</span><span style="color: blue">&gt;
                        </span>Welcome <span style="color: blue">&lt;</span><span style="color: maroon">span </span><span style="color: red">class</span><span style="color: blue">=&quot;bold&quot;&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LoginName </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeadLoginName&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;&lt;/</span><span style="color: maroon">span</span><span style="color: blue">&gt;</span>!
                        [ <span style="color: blue">&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LoginStatus </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeadLoginStatus&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">LogoutAction</span><span style="color: blue">=&quot;Redirect&quot; </span><span style="color: red">LogoutText</span><span style="color: blue">=&quot;Log Out&quot; </span><span style="color: red">LogoutPageUrl</span><span style="color: blue">=&quot;~/&quot;/&gt; </span>]
                    <span style="color: blue">&lt;/</span><span style="color: maroon">LoggedInTemplate</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LoginView</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;clear hideSkiplink&quot;&gt;
                &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Menu </span><span style="color: red">ID</span><span style="color: blue">=&quot;NavigationMenu&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;menu&quot; </span><span style="color: red">EnableViewState</span><span style="color: blue">=&quot;false&quot; </span><span style="color: red">IncludeStyleBlock</span><span style="color: blue">=&quot;false&quot; </span><span style="color: red">Orientation</span><span style="color: blue">=&quot;Horizontal&quot;&gt;
                    &lt;</span><span style="color: maroon">Items</span><span style="color: blue">&gt;
                        &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">MenuItem </span><span style="color: red">NavigateUrl</span><span style="color: blue">=&quot;~/Default.aspx&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Home&quot;/&gt;
                        &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">MenuItem </span><span style="color: red">NavigateUrl</span><span style="color: blue">=&quot;~/About.aspx&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;About&quot;/&gt;
                    &lt;/</span><span style="color: maroon">Items</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Menu</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;main&quot;&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;MainContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;/&gt;
        &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;clear&quot;&gt;
        &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;footer&quot;&gt;
        
    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">html</span><span style="color: blue">&gt;

</span></pre>

<p>&#160;</p>

<p>The Sys.Debug will now work:</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/01/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/01/image_thumb.png" width="780" height="473" /></a> </p>

<p>&#160;</p>

<p>&#160;</p>

<p>&#160;</p>

<p>&#160;</p>

<p><a href="http://11011.net/software/vspaste">&#160;</a></p>