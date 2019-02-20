---
ID: 1439
post_title: Custom error pages in ASP .NET 4.0
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/02/custom-error-pages-in-asp-net-4-0/
published: true
post_date: 2010-06-02 14:04:08
---
<p>If you want to use a custom error page in ASP .NET <strong>and</strong> want to show the exception details on that page, you must save the Server.GetLastError to a sessions variable in the Global.asax Application_Error event, manually clear the error and than manually redirect to a ErrorPage.aspx and do not use the Web.config “customErrors” tag.     <br />    <br /><strong>Global.asax</strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Web.Security;
<span style="color: blue">using </span>System.Web.SessionState;

<span style="color: blue">namespace </span>CustomBeheer
{
    <span style="color: blue">public class </span><span style="color: #2b91af">Global </span>: System.Web.<span style="color: #2b91af">HttpApplication
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Code that runs when an unhandled error occurs
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">void </span>Application_Error(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: green">// Catch exception and save to session variable, for displaying in ErrorPage.aspx
            </span><span style="color: #2b91af">Exception </span>ex = Server.GetLastError();
            <span style="color: blue">try
            </span>{
                <span style="color: green">// Session object is not always available, so use try finally block.
                // This will prevent recursive loop.
                </span>Session[<span style="color: #a31515">&quot;EncounteredException&quot;</span>] = ex;
            }
            <span style="color: blue">finally
            </span>{
                <span style="color: green">// To use the Session variable in ErrorPage.aspx we must clear the error and then manualy redirect to the ErrorPage.aspx.
                // Because we manualy redirect, we don't use the &quot;customErrors&quot; tag in the Web.config
                </span>Server.ClearError();
                Response.Redirect(<span style="color: #a31515">&quot;ErrorPage.aspx&quot;</span>);
            }
        }
    }
}</pre>



<p><strong>ErrorPage.aspx</strong></p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Web.UI;
<span style="color: blue">using </span>System.Web.UI.WebControls;

<span style="color: blue">namespace </span>Beheer
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">ErrorPage </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: green">//Exception ex = Server.GetLastError();
            </span><span style="color: blue">this</span>.ShowError();
        }
        <span style="color: blue">private void </span>ShowError()
        {
            <span style="color: #2b91af">Exception </span>encounteredException = Session[<span style="color: #a31515">&quot;EncounteredException&quot;</span>] <span style="color: blue">as </span><span style="color: #2b91af">Exception</span>;

            <span style="color: blue">if </span>(encounteredException != <span style="color: blue">null</span>)
            {
                Session[<span style="color: #a31515">&quot;EncounteredException&quot;</span>] = <span style="color: blue">null</span>;
                lblError.Text = encounteredException.ToString();
            }
        }
    }
}</pre>



<p><strong>[No changes to the Web.config]</strong></p>

<p><strong></strong></p>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image1.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb1.png" width="754" height="142" /></a></p>

<p>&#160;</p>

<p>The text: “Oops… something bad happened” is a predefined text and the “System.Web.HttpUnhandledException…” shows the exception details, catched in the global.asax Application_Error event.</p>

<p><strong>More on CustomErrorPages</strong></p>

<p><a title="http://aspnetresources.com/articles/CustomErrorPages.aspx" href="http://aspnetresources.com/articles/CustomErrorPages.aspx">http://aspnetresources.com/articles/CustomErrorPages.aspx</a></p>