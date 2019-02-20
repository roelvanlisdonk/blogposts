---
ID: 1265
post_title: >
  How to calculate the difference in
  seconds between 2 datetime strings
  (yyyyMMdd HHmmss) in a SSIS expression
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/21/how-to-calculate-the-difference-in-seconds-between-2-datetime-strings-yyyymmdd-hhmmss-in-a-ssis-expression/
published: true
post_date: 2010-04-21 08:53:55
---
<p>If you want to calculate the difference in seconds between 2 datetime strings (yyyyMMdd HHmmss) in a SSIS expression, you can use the following expression:</p>  <p>&#160;</p>  <p><strong>Pre</strong></p>  <p>@[User::StartDateTimeString] = “20100420 100000” </p>  <p>@[User::EndDateTimeString] = “20100420 101010”</p>  <p>&#160;</p>  <p><strong>Expression</strong></p>  <p>DATEDIFF(&quot;ss&quot;,(DT_DBTIMESTAMP)(SUBSTRING(@[User::StartDateTimeString],5,2) + &quot;/&quot; + SUBSTRING(@[User::StartDateTimeString],7,2) + &quot;/&quot; + SUBSTRING(@[User::StartDateTimeString],1,4) + &quot; &quot; + SUBSTRING(@[User::StartDateTimeString],10,2) + &quot;:&quot; + SUBSTRING(@[User::StartDateTimeString],12,2) + &quot;:&quot; + SUBSTRING(@[User::StartDateTimeString],14,2)),(DT_DBTIMESTAMP)(SUBSTRING(@[User::EndDateTimeString],5,2) + &quot;/&quot; + SUBSTRING(@[User::EndDateTimeString],7,2) + &quot;/&quot; + SUBSTRING(@[User::EndDateTimeString],1,4) + &quot; &quot; + SUBSTRING(@[User::EndDateTimeString],10,2) + &quot;:&quot; + SUBSTRING(@[User::EndDateTimeString],12,2) + &quot;:&quot; + SUBSTRING(@[User::EndDateTimeString],14,2)))</p>  <p>&#160;</p>  <p><strong>Result</strong></p>  <p>610</p>  <p>&#160;</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image25.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb25.png" width="604" height="498" /></a></p>