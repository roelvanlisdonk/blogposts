---
ID: 3533
post_title: >
  How to get all tablenames and
  columnsnames used in Outsystems with
  t-sql
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/11/05/how-to-get-all-tablenames-and-columnsnames-used-in-outsystems-with-t-sql/
published: true
post_date: 2013-11-05 14:14:08
---
<p>&#160;</p>  <pre class="code"><span style="color: blue">select      </span><span style="color: teal">e</span><span style="color: gray">.</span><span style="color: teal">NAME </span><span style="color: blue">as </span><span style="color: teal">TableName</span><span style="color: gray">, </span><span style="color: teal">ea</span><span style="color: gray">.</span><span style="color: teal">NAME </span><span style="color: blue">as </span><span style="color: teal">FieldName
</span><span style="color: blue">from        </span><span style="color: teal">[dbo]</span><span style="color: gray">.</span><span style="color: teal">[ossys_Entity] e
</span><span style="color: gray">inner join  </span><span style="color: teal">[dbo]</span><span style="color: gray">.</span><span style="color: teal">[ossys_Entity_Attr] ea </span><span style="color: blue">on </span><span style="color: teal">e</span><span style="color: gray">.</span><span style="color: teal">ID </span><span style="color: gray">= </span><span style="color: teal">ea</span><span style="color: gray">.</span><span style="color: magenta">ENTITY_ID
</span><span style="color: blue">where       </span><span style="color: teal">e</span><span style="color: gray">.</span><span style="color: teal">IS_ACTIVE </span><span style="color: gray">= </span>1
<span style="color: gray">and         </span><span style="color: teal">ea</span><span style="color: gray">.</span><span style="color: teal">IS_ACTIVE </span><span style="color: gray">= </span>1
<span style="color: blue">group by    </span><span style="color: teal">e</span><span style="color: gray">.</span><span style="color: teal">NAME</span><span style="color: gray">, </span><span style="color: teal">ea</span><span style="color: gray">.</span><span style="color: teal">Name
</span><span style="color: blue">order by    </span><span style="color: teal">TableName</span><span style="color: gray">, </span><span style="color: teal">FieldName
</span></pre>