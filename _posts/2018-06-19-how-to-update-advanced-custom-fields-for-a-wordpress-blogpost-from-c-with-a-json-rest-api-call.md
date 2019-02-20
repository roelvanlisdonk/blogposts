---
ID: 5211
post_title: 'How to update Advanced Custom Fields for a WordPress blogpost from C# with a JSON REST API call'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/06/19/how-to-update-advanced-custom-fields-for-a-wordpress-blogpost-from-c-with-a-json-rest-api-call/
published: true
post_date: 2018-06-19 13:44:25
---
<p>
 </p><p>When you want to edit the advanced custom fields for a WordPress blogpost, you must first install the ACF to REST API plugin.
</p><p>
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/06/061918_1144_Howtoupdate1.png" alt=""/>
	</p><p>
 </p><p>For sending authenticated POST request I used the JWT Autentication for WP-API plugin.
</p><p>(see https://www.roelvanlisdonk.nl/2018/06/18/how-to-create-wordpress-blog-posts-from-c-with-httpclient-and-the-wordpress-rest-api-on-docker-for-windows-10/)
</p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/06/061918_1144_Howtoupdate2.png" alt=""/>
	</p><p>
 </p><p>Now I have created a blogpost in WordPress and filled the advanced custom field: "my-field-1" with value: "value 1".
</p><p>The blogpost Id = 15.
</p><p>
 </p><p>To update the value, I used the following code:
</p><p>
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/06/061918_1144_Howtoupdate3.png" alt=""/>
	</p><p>
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/06/061918_1144_Howtoupdate4.png" alt=""/>
	</p><p>
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/06/061918_1144_Howtoupdate5.png" alt=""/>
	</p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p><p>
 </p>