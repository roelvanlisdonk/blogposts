---
ID: 1094
post_title: 'How to resolve: ListBox UI does not update (refresh) on WCF .NET Ria Services domaincontext async call in Silverlight 3'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/10/how-to-resolve-listbox-ui-does-not-update-refresh-on-wcf-net-ria-services-domaincontext-async-call-in-silverlight-3/
published: true
post_date: 2010-03-10 16:59:58
---
<p>When you are calling a function on a WCF .NET RIA service, the completed eventhandler will take you back to the UI thread, but if you are binding the ListBox to a List&lt;….&gt; the UI of the Listbox won’t be updated.</p>  <p>Solution: don’t use a List&lt;…&gt; as ItemSource but a System.Collections.ObjectModel.ObservableCollection&lt;…&gt;</p>