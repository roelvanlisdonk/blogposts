---
ID: 4068
post_title: >
  Using ValidateAntiForgeryToken with
  AngularJS and MVC
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/10/23/using-validateantiforgerytoken-with-angularjs-and-mvc/
published: true
post_date: 2014-10-23 07:43:52
---
<p align="left">I was getting a HTTP 500 error, when posting data from AngularJS to a MVC controller, which had the attribute <strong>ValidateAntiForgeryToken</strong> applied to it. This attribute expects a form to be posted to the MVC controller action method, but I wanted to sent JSON. If you want to do that then you can follow the blogpost from julian jelfs.</p>  <p align="left">&#160;</p>  <p align="left">Now I just add: @Html.AntiForgeryToken()</p>  <p align="left">Then I apply the custom attribute ValidateJsonAntiForgeryToken to the MVC controller action method, like </p>  <pre class="code"><span style="background: white; color: black">[</span><span style="background: white; color: #2b91af">HttpPost</span><span style="background: white; color: black">]<br /><span style="background: white; color: black">[</span><span style="background: white; color: #2b91af">Authorize</span><span style="background: white; color: black">] </span>
[<font color="#4bacc6"><span style="background: white; color: #2b91af">ValidateJsonAntiForgeryToken</span></font>]
</span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">ActionResult </span><span style="background: white; color: black">GetDashboardData(DashboardViewModel model)
{</span></pre>


<p align="left">Now I can Post data in AngularJS like:</p>

<pre class="code"><span style="background: white; color: green">// When using the @Html.AntiForgeryToken() and [ValidateJsonAntiForgeryToken], a http POST, <br />// should contain a AntiForgeryToken in the header.
// The @Html.AntiForgeryToken() will write add a hidden HTML input element with the name <br />//&quot;__RequestVerificationToken&quot;.
// This input element will contain to AntiForgeryToken.
// The MVC AuthorizeAttribute [ValidateJsonAntiForgeryToken], <br />//will check the http request header for the &quot;AntiForgeryToken&quot;.
        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">getHttpConfig() {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">token = angular.element(</span><span style="background: white; color: #a31515">&quot;input[name='__RequestVerificationToken']&quot;</span><span style="background: white; color: black">).val();
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">config = {
                headers: {
                    </span><span style="background: white; color: #a31515">'__RequestVerificationToken'</span><span style="background: white; color: black">: token
                }
            };
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">config;
        }</span></pre>


<pre class="code"><p><span style="background: white; color: blue">var </span><span style="background: white; color: black">config = getHttpConfig();<br /><span style="background: white; color: blue">var </span><span style="background: white; color: black">url = “http://localhost”; </span></span><span style="background: white; color: black">
<span style="background: white; color: blue">var </span><span style="background: white; color: black">postData = {}; </span>            
</span><span style="background: white; color: blue">return </span><span style="background: white; color: black">$http.post(url, postData, config).then(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(response) {<br />// Do something terrible
    </span><span style="background: white; color: black">});</span></p></pre>


<p align="left">&#160;</p>

<p><strong>Solution</strong></p>

<p>&#160;</p>

<p><a title="https://julianjelfs.wordpress.com/category/mvc/" href="https://julianjelfs.wordpress.com/category/mvc/">https://julianjelfs.wordpress.com/category/mvc/</a></p>