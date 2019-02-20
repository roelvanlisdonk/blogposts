---
ID: 3305
post_title: >
  Generate SQL insert statements from
  Excel / Csv file online
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/06/27/generate-sql-statements-from-excel-csv-file-online/
published: true
post_date: 2013-06-27 16:18:41
---
<p>Lets say you get a Microsoft Excel file containing the following information:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image20.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb20.png" width="579" height="640" /></a></p>  <p>&#160;</p>  <p>If you want to import these record in a SQL table, just save the excel file as CSV.</p>  <p>Then upload it to <a href="http://www.convertcsvtomysql.com/">http://www.convertcsvtomysql.com/</a></p>  <p>&#160;</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image21.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb21.png" width="549" height="604" /></a></p>  <p>&#160;</p>  <p>This will generate the following SQL script:</p>  <p>CREATE TABLE IF NOT EXISTS 'product'   <br />(    <br />'name' VARCHAR(255) NOT NULL,    <br />'description' VARCHAR(255) NOT NULL    <br />)</p>  <p>INSERT INTO 'product' VALUES   <br />('Car', 'This is the car description'),    <br />('Bike', 'This is the bike description'),    <br />('Bus', 'This is the bus description');</p>  <p>&#160;</p>  <p>Remove the &quot;create table&quot; peace if your table already exists.</p>