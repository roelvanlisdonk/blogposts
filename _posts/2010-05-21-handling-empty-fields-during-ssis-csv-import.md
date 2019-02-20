---
ID: 1424
post_title: >
  Handling empty fields during SSIS CSV
  import
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/05/21/handling-empty-fields-during-ssis-csv-import/
published: true
post_date: 2010-05-21 11:23:13
---
<p>Just a reminder:   <br />    <br />If you have a CSV file containing the data:</p>  <p>DataInColumn1Row1,DataInColumn2Row1,DataInColumn3Row1   <br />,DataInColumn2Row2,DataInColumn3Row2    <br />DataInColumn1Row3,DataInColumn2Row3,    <br />DataInColumn1Row4,,DataInColumn3Row4</p>  <p>and you import the columns using a SSIS package the empty columns will be converted to an empty string (“”) and not NULL. </p>