---
ID: 1862
post_title: >
  Convert object to string by using
  XmlSerializer
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/07/convert-object-to-string-by-using-xmlserializer/
published: true
post_date: 2011-01-07 13:16:46
---
<p>If you want to convert a custom object [Product] to a string by using the XmlSerializer class, you can use the StringWriter class like:</p>  <pre class="code"><span style="color: #2b91af">           StringBuilder </span>result = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

           <span style="color: green">// Get the product from filesystem
           </span><span style="color: #2b91af">Product </span>product = Load();

           <span style="color: green">// Convert object to string by using XmlSerializer
           </span><span style="color: blue">using </span>(<span style="color: #2b91af">StringWriter </span>writer = <span style="color: blue">new </span><span style="color: #2b91af">StringWriter</span>(result))
           {
               <span style="color: #2b91af">XmlSerializer </span>xs = <span style="color: blue">new </span><span style="color: #2b91af">XmlSerializer</span>(<span style="color: blue">typeof</span>(<span style="color: #2b91af">Product</span>));
               xs.Serialize(writer, product);
           }</pre>
<a href="http://11011.net/software/vspaste"></a>