---
ID: 1448
post_title: Using the Telerik GridHyperlinkColumn
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/14/using-the-telerik-gridhyperlinkcolumn/
published: true
post_date: 2010-06-14 16:45:10
---
<p align="left">I wanted a GridHyperlinkColumn to have a static text</p>  <p align="left">&#160;</p>  <p align="left"><strong>DataTextField</strong>, contains the datasource columns that can be used in the property “DataTextFormatString”</p>  <p align="left"><strong>DataTextFormatString</strong>, is used to display the text of the hyperlink. Must be set, else the column would be empty!</p>  <p align="left"><strong>DataNavigateUrlFields</strong>, contains the datasource columns that can be used in the property “DataNavigateUrlFormatString”</p>  <p align="left"><strong>DataNavigateUrlFormatString</strong>, is used to set the href property of the link</p>  <p align="left">&#160;</p>  <p align="left">The following column will show the text “Edit” for each row. The href of each link will by dynamically set. Example link would be <strong>&lt;a href=”http://localhost/CustomerDetail.aspx?CustomerId=112”&gt;Edit&lt;/a&gt;</strong>&#160;</p>  <p align="left">&#160;</p>  <div align="left">   <pre class="code"><span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridHyperlinkColumn
                    </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;EditColumn&quot;
                    </span><span style="color: red">DataTextFormatString</span><span style="color: blue">=&quot;Edit&quot;
                    </span><span style="color: red">DataTextField</span><span style="color: blue">=&quot;Name&quot;
                    </span><span style="color: red">DataNavigateUrlFields</span><span style="color: blue">=&quot;Id&quot;
                    </span><span style="color: red">DataNavigateUrlFormatString</span><span style="color: blue">=&quot;~/CustomerDetail.aspx?CustomerId={0}&quot;
                    </span><span style="color: red">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;CustomerEditColumn&quot;&gt;
                &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridHyperlinkColumn</span><span style="color: blue">&gt;
</span></pre>
</div>
<a href="http://11011.net/software/vspaste"></a>