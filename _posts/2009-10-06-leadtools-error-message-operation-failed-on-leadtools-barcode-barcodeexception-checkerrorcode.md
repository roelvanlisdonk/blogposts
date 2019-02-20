---
ID: 741
post_title: 'Leadtools error message &#8220;Operation failed&#8221; on Leadtools.Barcode.BarcodeException.CheckErrorCode'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/06/leadtools-error-message-operation-failed-on-leadtools-barcode-barcodeexception-checkerrorcode/
published: true
post_date: 2009-10-06 17:02:38
---
<p>If you get the leadtools error message “Operation failed” in function Leadtools.Barcode.BarcodeException.CheckErrorCode, you should check if the following files are in the same folder as the assemlby that uses the leadtools assemblies:   <br />    <br /><strong>Leadtools .NET assemblies:     <br /></strong>Leadtools.Barcode.dll    <br />Leadtools.Codecs.dll    <br />Leadtools.dll    <br />Leadtools.Forms.dll    <br />Leadtools.Forms.Ocr.dll    <br />Leadtools.Forms.Ocr.Plus.dll    <br />Leadtools.ImageProcessing.Core.dll    <br />Leadtools.ImageProcessing.Utilities.dll    <br />    <br /><strong>Leadtools not .NET assemblies:     <br /></strong>Ltbar4u.dll    <br />Ltbar6ru.dll    <br />Ltbar6wu.dll    <br />Ltbar7ru.dll    <br />Ltbar7wu.dll    <br />Ltbar8ru.dll    <br />Ltbar8wu.dll    </p>