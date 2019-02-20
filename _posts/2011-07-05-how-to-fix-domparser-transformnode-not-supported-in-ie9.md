---
ID: 2113
post_title: 'How to fix: DOMParser.TransformNode not supported in IE9'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/07/05/how-to-fix-domparser-transformnode-not-supported-in-ie9/
published: true
post_date: 2011-07-05 16:12:04
---
<p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/07/clip_image002.jpg" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="clip_image002" border="0" alt="clip_image002" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/07/clip_image002_thumb.jpg" width="415" height="163" /></a></p>  <p>&#160;</p>  <p>This issue can be fixed in IE9 by using the following javascript function:</p>  <p>&#160;</p>  <pre class="code"><span style="color: #006400">/*
Transforms a XML document to a HTML string by using a XSLT document
1. Use type XSLTProcessor, if browser (FF, Safari, Chrome etc) supports it
2. Use function [transformNode] on the XmlDocument, if browser (IE6, IE7, IE8) supports it
3. Use function transform on the XsltProcessor used for IE9 (which doesn't support [transformNode] any more) 
4. Throws an error, when both types are not supported
*/
</span><span style="color: blue">function </span>TransformToHtmlText(xmlDoc, xsltDoc) {
    <span style="color: #006400">// 1.
    </span><span style="color: blue">if </span>(<span style="color: blue">typeof </span>(XSLTProcessor) != <span style="color: maroon">&quot;undefined&quot;</span>) {
        <span style="color: blue">var </span>xsltProcessor = <span style="color: blue">new </span>XSLTProcessor();
        xsltProcessor.importStylesheet(xsltDoc);
        <span style="color: blue">var </span>xmlFragment = xsltProcessor.transformToFragment(xmlDoc, document);
        <span style="color: blue">return </span>GetXmlStringFromXmlDoc(xmlFragment);
    }
    <span style="color: #006400">// 2.
    </span><span style="color: blue">if </span>(<span style="color: blue">typeof </span>(xmlDoc.transformNode) != <span style="color: maroon">&quot;undefined&quot;</span>) {
        <span style="color: blue">return </span>xmlDoc.transformNode(xsltDoc);
    }
    <span style="color: blue">else </span>{

        <span style="color: blue">try </span>{
            <span style="color: #006400">// 3
            </span><span style="color: blue">if </span>(window.ActiveXObject) {
                <span style="color: blue">var </span>xslt = <span style="color: blue">new </span>ActiveXObject(<span style="color: maroon">&quot;Msxml2.XSLTemplate&quot;</span>);
                <span style="color: blue">var </span>xslDoc = <span style="color: blue">new </span>ActiveXObject(<span style="color: maroon">&quot;Msxml2.FreeThreadedDOMDocument&quot;</span>);
                xslDoc.loadXML(xsltDoc.xml);
                xslt.stylesheet = xslDoc;
                <span style="color: blue">var </span>xslProc = xslt.createProcessor();
                xslProc.input = xmlDoc;
                xslProc.transform();

                <span style="color: blue">return </span>xslProc.output;
            }
        }
        <span style="color: blue">catch </span>(e) {
            <span style="color: #006400">// 4
            </span>alert(<span style="color: maroon">&quot;The type [XSLTProcessor] and the function [XmlDocument.transformNode] are not supported by this browser, can't transform XML document to HTML string!&quot;</span>);
            <span style="color: blue">return null</span>;
        }

    }
}</pre>