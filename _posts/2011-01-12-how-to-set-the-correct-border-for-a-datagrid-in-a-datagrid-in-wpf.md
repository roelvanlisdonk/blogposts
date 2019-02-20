---
ID: 1877
post_title: >
  How to set the correct border for a
  datagrid in a datagrid in WPF
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/12/how-to-set-the-correct-border-for-a-datagrid-in-a-datagrid-in-wpf/
published: true
post_date: 2011-01-12 13:59:19
---
<p>If you use a datagrid in the DataGrid.RowDetailsTemplate and set the last column width to * and the datagrid is set to HorizontalAlignment=&quot;Stretch&quot;, then you might get a horizontal scrollbar. To prevent this, set the HorizontalScrollBarVisibility=&quot;Disabled&quot; on the top datagrid and subdatagrids</p>  <p>&#160;</p>  <p>The first screendump show the datagrids with HorizontalScrollBarVisibility set to “Enabled”, as you can see at the bottom of the screendump, the datagrid contains a horizontal scrollbar. This is, because the last column width is set to *.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/01/image3.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/01/image_thumb3.png" width="746" height="588" /></a> </p>  <p>The second screendump shows the correct layout (with HorizontalScrollBarVisibility set to &quot;Disabled&quot;)</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/01/image4.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/01/image_thumb4.png" width="732" height="605" /></a></p>