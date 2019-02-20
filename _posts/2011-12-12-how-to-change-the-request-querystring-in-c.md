---
ID: 2289
post_title: 'How to change the Request.QueryString in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/12/how-to-change-the-request-querystring-in-c/
published: true
post_date: 2011-12-12 12:01:24
---
<p>If you want to post back to the same page, only adjusting the query string parameters, you can use the following code:</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Specialized;
<span style="color: blue">using </span>System.Web;

<span style="color: blue">namespace </span>WebApplication1
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">_Default </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
        }

        <span style="color: blue">protected void </span>GoLinkButton_Click(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: green">// Copy the original querystring parameters.
            </span><span style="color: #2b91af">NameValueCollection </span>queryString = <span style="color: #2b91af">HttpUtility</span>.ParseQueryString(Request.QueryString.ToString());

            <span style="color: green">// Set the first parameter (it will be added if it does not exist).
            </span>queryString.Set(<span style="color: #a31515">&quot;myparameter1&quot;</span>, <span style="color: #a31515">&quot;1000&quot;</span>);                          
            
            <span style="color: green">// Postback to the same page, with adjusted querystring parameters.
            </span>Response.Redirect(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}?{1}&quot;</span>, Request.Url, queryString.ToString()));
        }
    }
}</pre>


<p>Before click on the Go button:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image7.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb7.png" width="580" height="278" /></a></p>

<p>&#160;</p>

<p>After click on the Go button:</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image8.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb8.png" width="580" height="263" /></a></p>