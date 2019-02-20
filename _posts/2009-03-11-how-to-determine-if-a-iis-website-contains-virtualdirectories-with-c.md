---
ID: 276
post_title: 'How to determine if an IIS website contains virtualdirectories, with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/11/how-to-determine-if-a-iis-website-contains-virtualdirectories-with-c/
published: true
post_date: 2009-03-11 14:52:16
---
<p></p><pre class="code"><span style="color:gray;">       /// &lt;summary&gt;
       /// </span><span style="color:green;">Does the given IIS website contain virtualdirectories.
       </span><span style="color:gray;">/// &lt;/summary&gt;
       /// &lt;returns&gt;&lt;/returns&gt;
       </span><span style="color:blue;">public bool </span>DoesWebsiteContainVirtualDirectories(<span style="color:blue;">string </span>website)
       {
           <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(website)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [website] can't be null or empty"</span>); }
           <span style="color:blue;">bool </span>result = <span style="color:blue;">false</span>;

           <span style="color:#2b91af;">DirectoryEntry </span>w3svc = <span style="color:blue;">new </span><span style="color:#2b91af;">DirectoryEntry</span>(<span style="color:#a31515;">"IIS://localhost/w3svc"</span>);

           <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>site <span style="color:blue;">in </span>w3svc.Children)
           {
               <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>] != <span style="color:blue;">null</span>)
               {
                   <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value != <span style="color:blue;">null</span>)
                   {
                       <span style="color:blue;">if </span>(site.SchemaClassName.Equals(<span style="color:#a31515;">"IIsWebServer") </span>&amp;&amp; site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value.ToString().Equals(website))
                       {
                           <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>child <span style="color:blue;">in </span>site.Children)
                           {
                               <span style="color:blue;">if </span>(!result)
                               {
                                   <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">PropertyValueCollection </span>property <span style="color:blue;">in </span>child.Properties)
                                   {
                                       <span style="color:blue;">if </span>(property.Value != <span style="color:blue;">null</span>)
                                       {
                                           <span style="color:blue;">if </span>(property.PropertyName.Equals(<span style="color:#a31515;">"KeyType"</span>) &amp;&amp; property.Value.ToString().Equals(<span style="color:#a31515;">"IIsWebVirtualDir"</span>))
                                           {
                                               <span style="color:blue;">return true</span>;
                                           }
                                       }
                                   }
                               }
                           }
                       }
                   }
               }
           }

           <span style="color:blue;">return </span>result;
       }</pre><a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>