---
ID: 2180
post_title: 'Solving: Add and delete buttons on the DataForm are disabled when using an List&lt;Entity&gt; as ItemSoure'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/10/25/solving-add-and-delete-buttons-on-the-dataform-are-disabled-when-using-an-listentity-as-itemsoure/
published: true
post_date: 2011-10-25 11:13:16
---
<p>&#160;</p>  <p>When you bind the DataForm.ItemSource directly to an entity set returned from your RIA DomainService, the DataForm add and delete buttons are disabled. This is caused by the implementation in RIA Services of the entity sets. If you use an ObserverableCollection the buttons are enabled, found mine solution at: <a title="http://forums.silverlight.net/t/190405.aspx/1" href="http://forums.silverlight.net/t/190405.aspx/1">http://forums.silverlight.net/t/190405.aspx/1</a></p>