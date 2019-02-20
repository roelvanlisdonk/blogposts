---
ID: 856
post_title: >
  How to copy XML nodes between documents
  (use ImportNode)
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/16/how-to-copy-xml-nodes-between-documents-use-importnode/
published: true
post_date: 2009-12-16 15:27:56
---
<p><a title="http://www.geekpedia.com/tutorial150_How-to-copy-XML-nodes-between-documents.html" href="http://www.geekpedia.com/tutorial150_How-to-copy-XML-nodes-between-documents.html">http://www.geekpedia.com/tutorial150_How-to-copy-XML-nodes-between-documents.html</a>    <br />    <br />To copy node between XmlDocuments use importnode:    <br />// Store the root node of the destination document into an XmlNode    <br />// The 1 in ChildNodes[1] is the index of the node to be copied (where 0 is the first node)    <br />XmlNode rootDest = myDestDoc[&quot;DestinationRoot&quot;];    <br />// Store the node to be copied into an XmlNode    <br />XmlNode nodeOrig = mySourceDoc[&quot;SourceRoot&quot;].ChildNodes[1];    <br />// Store the copy of the original node into an XmlNode    <br />XmlNode nodeDest = myDestDoc.ImportNode(nodeOrig, true);    <br />// Append the node being copied to the root of the destination document    <br />rootDest.AppendChild(nodeDest);</p>