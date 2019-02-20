---
ID: 1986
post_title: 'Solving: Object reference not set to an instance of an object, when calling a WCF service'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/04/18/solving-object-reference-not-set-to-an-instance-of-an-object-when-calling-a-wcf-service/
published: true
post_date: 2011-04-18 13:27:45
---
<p>&#160;</p>  <p>I was getting a [<strong>Object reference not set to an instance of an object.</strong>] error, when calling a WCF service from a client application. The WCF service was build in [Any CPU] configuration, but an external dll was build in x86 modus. In this case the WCF service will only work, when you set the application pool property [<strong>Enable 32-Bit Applications</strong>] to <strong>True</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/04/image3.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/04/image_thumb3.png" width="362" height="440" /></a></p>  <p>&#160;</p>  <p>&#160;</p>  <p>&#160;</p>  <h3>Exception</h3>  <p>[Object reference not set to an instance of an object.]   <br />Server stack trace:    <br />System.ServiceModel.Channels.ServiceChannel.ThrowIfFaultUnderstood    <br />System.ServiceModel.Channels.ServiceChannel.HandleReply    <br />System.ServiceModel.Channels.ServiceChannel.Call    <br />System.ServiceModel.Channels.ServiceChannelProxy.InvokeService    <br />System.ServiceModel.Channels.ServiceChannelProxy.Invoke    <br />Exception rethrown[0]:    <br />System.Runtime.Remoting.Proxies.RealProxy.HandleReturnMessage    <br />System.Runtime.Remoting.Proxies.RealProxy.PrivateInvoke</p>