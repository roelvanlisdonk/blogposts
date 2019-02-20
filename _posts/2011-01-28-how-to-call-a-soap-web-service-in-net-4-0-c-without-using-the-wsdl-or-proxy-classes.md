---
ID: 1893
post_title: 'How to call a SOAP web service in .NET 4.0 C# without using the WSDL or proxy classes'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/28/how-to-call-a-soap-web-service-in-net-4-0-c-without-using-the-wsdl-or-proxy-classes/
published: true
post_date: 2011-01-28 10:16:45
---
<p>If you want to call a .NET 4.0 C# web service, without using the WSDL or “Add Service Reference” in Microsoft Visual Studio 2010. You can use the following functions:</p>  <pre class="code"><span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Execute a Soap WebService call
</span><span style="color: gray">/// &lt;/summary&gt;
</span><span style="color: blue">public override void </span>Execute()
{
    <span style="color: #2b91af">HttpWebRequest </span>request = CreateWebRequest();
    <span style="color: #2b91af">XmlDocument </span>soapEnvelopeXml = <span style="color: blue">new </span><span style="color: #2b91af">XmlDocument</span>();
    soapEnvelopeXml.LoadXml(<span style="color: #a31515">@&quot;&lt;?xml version=&quot;&quot;1.0&quot;&quot; encoding=&quot;&quot;utf-8&quot;&quot;?&gt;
&lt;soap:Envelope xmlns:soap=&quot;&quot;http://schemas.xmlsoap.org/soap/envelope/&quot;&quot; xmlns:xsi=&quot;&quot;http://www.w3.org/2001/XMLSchema-instance&quot;&quot; xmlns:xsd=&quot;&quot;http://www.w3.org/2001/XMLSchema&quot;&quot;&gt;
&lt;soap:Body&gt;
    &lt;HelloWorld3 xmlns=&quot;&quot;http://tempuri.org/&quot;&quot;&gt;
        &lt;parameter1&gt;test&lt;/parameter1&gt;
        &lt;parameter2&gt;23&lt;/parameter2&gt;
        &lt;parameter3&gt;test&lt;/parameter3&gt;
    &lt;/HelloWorld3&gt;
&lt;/soap:Body&gt;
&lt;/soap:Envelope&gt;&quot;</span>);
            
    <span style="color: blue">using </span>(<span style="color: #2b91af">Stream </span>stream = request.GetRequestStream()) 
    { 
        soapEnvelopeXml.Save(stream); 
    }

    <span style="color: blue">using </span>(<span style="color: #2b91af">WebResponse </span>response = request.GetResponse())
    {
        <span style="color: blue">using </span>(<span style="color: #2b91af">StreamReader </span>rd = <span style="color: blue">new </span><span style="color: #2b91af">StreamReader</span>(response.GetResponseStream())) 
        { 
            <span style="color: blue">string </span>soapResult = rd.ReadToEnd();
            <span style="color: #2b91af">Console</span>.WriteLine(soapResult);
        } 
    }
}
<span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Create a soap webrequest to [Url]
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;returns&gt;&lt;/returns&gt;
</span><span style="color: blue">public </span><span style="color: #2b91af">HttpWebRequest </span>CreateWebRequest()
{
    <span style="color: #2b91af">HttpWebRequest </span>webRequest = (<span style="color: #2b91af">HttpWebRequest</span>)<span style="color: #2b91af">WebRequest</span>.Create(<span style="color: #a31515">@&quot;http://dev.nl/Rvl.Demo.TestWcfServiceApplication/SoapWebService.asmx&quot;</span>); 
    webRequest.Headers.Add(<span style="color: #a31515">@&quot;SOAP:Action&quot;</span>); 
    webRequest.ContentType = <span style="color: #a31515">&quot;text/xml;charset=\&quot;utf-8\&quot;&quot;</span>; 
    webRequest.Accept = <span style="color: #a31515">&quot;text/xml&quot;</span>; 
    webRequest.Method = <span style="color: #a31515">&quot;POST&quot;</span>; 
    <span style="color: blue">return </span>webRequest; 
}</pre>


<p>Result</p>

<p>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&lt;soap:Envelope xmlns:soap=&quot;<a href="http://schemas.xmlsoap.org/soap/envelope/&quot;">http://schemas.xmlsoap.org/soap/envelope/&quot;</a> xmlns:xsi=&quot;<a href="http://www.w3.org/2001/XMLSchema-instance&quot;">http://www.w3.org/2001/XMLSchema-instance&quot;</a> xmlns:xsd=&quot;<a href="http://www.w3.org/2001/XMLSchema&quot;">http://www.w3.org/2001/XMLSchema&quot;</a>&gt;&lt;soap:Body&gt;&lt;HelloWorld3Response xmlns=&quot;<a href="http://tempuri.org/&quot;">http://tempuri.org/&quot;</a>&gt;&lt;HelloWorld3Result&gt;test&lt;/HelloWorld3Result&gt;&lt;/HelloWorld3Response&gt;&lt;/soap:Body&gt;&lt;/soap:Envelope&gt;</p>

<p>&#160;</p>

<p>You can use complex types in you’re request. I use fiddler to get the contents of the soap envelope.</p>