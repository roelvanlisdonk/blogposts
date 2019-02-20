---
ID: 1572
post_title: >
  Button click event causes a
  RequiredFieldValidator to fire in an ASP
  .NET DetailsView
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/28/button-click-event-causes-a-requiredfieldvalidator-to-fire-in-an-asp-net-detailsview/
published: true
post_date: 2010-06-28 14:07:52
---
<p>If you use a linkbutton and a RequiredFieldValidator in an ASP .NET DetailsView template column. The linkbutton click event causes the RequiredFieldValidator to fire. If you don’t want the RequiredFieldValidator to fire when you push the linkbutton, set the CausesValidation property to false.</p>  <pre class="code"><span style="color: red">CausesValidation</span><span style="color: blue">=&quot;false&quot;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>