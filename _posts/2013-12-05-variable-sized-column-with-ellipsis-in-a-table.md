---
ID: 3589
post_title: >
  Variable sized column with ellipsis in a
  table
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/12/05/variable-sized-column-with-ellipsis-in-a-table/
published: true
post_date: 2013-12-05 10:37:48
---
<p>If you want a column of a table in HTML to expand and you want the text to show &quot;ellipsis&quot; for overflowing text, you can use the solution found at: </p>  <p>&#160;</p>  <p><a href="http://stackoverflow.com/questions/17345158/variable-sized-column-with-ellipsis-in-a-table">http://stackoverflow.com/questions/17345158/variable-sized-column-with-ellipsis-in-a-table</a></p>  <p>&#160;</p>  <p>Just give each cell for the specific column the following class:</p>  <pre class="code"><span style="background: white; color: maroon">.expand-column
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">max-width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">overflow</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">hidden</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-ms-text-overflow</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">ellipsis</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-o-text-overflow</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">ellipsis</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">text-overflow</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">ellipsis</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">white-space</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">nowrap</span><span style="background: white; color: black">;
        }</span></pre>