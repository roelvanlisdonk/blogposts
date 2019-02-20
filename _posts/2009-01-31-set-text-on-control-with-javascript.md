---
ID: 242
post_title: Set text on control with javascript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/01/31/set-text-on-control-with-javascript/
published: true
post_date: 2009-01-31 10:59:55
---
<p>To set the text on a control with javascript use:</p> <p>&nbsp;</p><pre class="code"><span style="color:green;">/*
    Set the text value of the given element.
    This function assumes this document is defined and not null and has a function getElementById
    Used by: -
*/
</span><span style="color:blue;">function </span>SetText(elementId, text)
{
    <span style="color:green;">// Check input values
    </span><span style="color:blue;">if</span>(IsNullOrUndefined(document)){alert(<span style="color:#a31515;">'SetText: Object [document] is null or undefined'</span>);}
    <span style="color:blue;">if</span>(IsNullOrUndefined(elementId)){alert(<span style="color:#a31515;">'SetText: Object [elementId] is null or undefined'</span>);}
    <span style="color:blue;">if</span>(IsNullOrUndefined(text)){text = <span style="color:#a31515;">''</span>;}

    <span style="color:green;">// Get the given element by id
    </span><span style="color:blue;">var </span>resultGetElementById = document.getElementById(elementId);
    <span style="color:blue;">if</span>(IsNullOrUndefined(resultGetElementById)){alert(<span style="color:#a31515;">'SetText: Object [resultGetElementById] is null or undefined'</span>);}

    <span style="color:green;">// Check if the firstChild is null or undefined
    </span><span style="color:blue;">if</span>(IsNullOrUndefined(resultGetElementById.firstChild))
    {
        <span style="color:green;">// Element does not have a first node, add an textnode.
        </span>resultGetElementById.appendChild(document.createTextNode(text));
    }
    <span style="color:blue;">else
    </span>{
        <span style="color:green;">// Element has a first childe node, so replace it's text value.
        </span>resultGetElementById.firstChild.nodeValue = text;
    }
}</pre><a href="http://11011.net/software/vspaste"></a>