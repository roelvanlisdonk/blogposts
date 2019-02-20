---
ID: 5129
post_title: >
  How to use server sorting with jquery
  datatable
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/11/02/how-to-use-server-sorting-with-jquery-datatable/
published: true
post_date: 2017-11-02 13:32:47
---
<p>If you are using jquery datatables found at ... and you want to display the data as it was returned from the server explicitly set datatable options "order" to: [].
</p><p>https://datatables.net/reference/option/order
</p><p>
 </p><p><span style="color:#333333; font-size:10pt"><span style="font-family:Courier New">$(<span style="background-color:#f5eee9">'#example'</span>).dataTable( {</span><span style="font-family:Consolas">
			</span></span></p><p><span style="color:#444444; font-size:10pt"><span style="font-family:Courier New">    <span style="color:#333333"><span style="background-color:#f5eee9">"order"</span>: []</span></span><span style="font-family:Consolas">
			</span></span></p><p><span style="color:#333333; font-size:10pt"><span style="font-family:Courier New">} );</span><span style="font-family:Consolas">
			</span></span></p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p>