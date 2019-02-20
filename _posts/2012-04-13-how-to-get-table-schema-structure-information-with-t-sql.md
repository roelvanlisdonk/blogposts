---
ID: 2651
post_title: >
  How to get table schema / structure
  information with T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/04/13/how-to-get-table-schema-structure-information-with-t-sql/
published: true
post_date: 2012-04-13 11:47:15
---
<p>If you want to get table schema / structure information with T-SQL, you have several options, the most commonly used by me are:</p>  <p><strong>Using the system stored procedure sp_help</strong></p>  <p>exec sp_help '&lt;your table name&gt;'</p>  <p>&#160;</p>  <p><strong>Using a custom query</strong></p>   <pre class="code"><span style="color: green">-- Dump table schema / structure info
</span><span style="color: blue">declare </span><span style="color: teal">@tabelObjectId </span><span style="color: blue">int
set </span><span style="color: teal">@tabelObjectId </span><span style="color: gray">= </span><span style="color: magenta">Object_ID</span><span style="color: gray">(</span><span style="color: red">N'&lt;Your table name&gt;'</span><span style="color: gray">)

</span><span style="color: blue">select
  </span><span style="color: red">'Column_name' </span><span style="color: gray">= </span><span style="color: teal">ac</span><span style="color: gray">.</span><span style="color: teal">name</span><span style="color: gray">,
  </span><span style="color: red">'Type'        </span><span style="color: gray">= </span><span style="color: magenta">type_name</span><span style="color: gray">(</span><span style="color: teal">ac</span><span style="color: gray">.</span><span style="color: teal">user_type_id</span><span style="color: gray">),
  </span><span style="color: red">'Length'            </span><span style="color: gray">= </span><span style="color: magenta">convert</span><span style="color: gray">(</span><span style="color: blue">int</span><span style="color: gray">, </span><span style="color: teal">ac</span><span style="color: gray">.</span><span style="color: teal">max_length</span><span style="color: gray">),
  </span><span style="color: red">'Nullable'        </span><span style="color: gray">= </span><span style="color: blue">case when </span><span style="color: teal">ac</span><span style="color: gray">.</span><span style="color: teal">is_nullable </span><span style="color: gray">= </span>0 <span style="color: blue">then </span><span style="color: red">'No' </span><span style="color: blue">else </span><span style="color: red">'Yes' </span><span style="color: blue">end</span><span style="color: gray">,
  </span><span style="color: red">'Identity'    </span><span style="color: gray">= </span><span style="color: blue">case when </span><span style="color: teal">ac</span><span style="color: gray">.</span><span style="color: teal">is_identity </span><span style="color: gray">= </span>0 <span style="color: blue">then </span><span style="color: red">'No' </span><span style="color: blue">else </span><span style="color: red">'Yes' </span><span style="color: blue">end</span><span style="color: gray">,
  </span><span style="color: red">'PK'          </span><span style="color: gray">= </span><span style="color: blue">case when </span><span style="color: gray">exists(
                    </span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: lime">sys</span><span style="color: gray">.</span><span style="color: lime">index_columns </span><span style="color: teal">ic
                    </span><span style="color: gray">inner join </span><span style="color: lime">sys</span><span style="color: gray">.</span><span style="color: lime">columns </span><span style="color: teal">c  </span><span style="color: blue">on  </span><span style="color: teal">ic</span><span style="color: gray">.</span><span style="color: magenta">object_id </span><span style="color: gray">= </span><span style="color: teal">c</span><span style="color: gray">.</span><span style="color: magenta">object_id
                                              </span><span style="color: gray">and </span><span style="color: teal">c</span><span style="color: gray">.</span><span style="color: teal">column_id </span><span style="color: gray">= </span><span style="color: teal">ic</span><span style="color: gray">.</span><span style="color: teal">column_id
                    </span><span style="color: blue">where </span><span style="color: teal">ic</span><span style="color: gray">.</span><span style="color: magenta">object_id </span><span style="color: gray">= </span><span style="color: teal">@tabelObjectId </span><span style="color: gray">and </span><span style="color: teal">c</span><span style="color: gray">.</span><span style="color: teal">name </span><span style="color: gray">= </span><span style="color: teal">ac</span><span style="color: gray">.</span><span style="color: teal">name
                  </span><span style="color: gray">) </span><span style="color: blue">then </span><span style="color: red">'Yes' </span><span style="color: blue">else </span><span style="color: red">'No' </span><span style="color: blue">end</span><span style="color: gray">,
  </span><span style="color: red">'FK'          </span><span style="color: gray">= </span><span style="color: blue">case when </span><span style="color: gray">exists(
                    </span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: lime">sys</span><span style="color: gray">.</span><span style="color: lime">foreign_key_columns </span><span style="color: teal">fc
                    </span><span style="color: gray">inner join </span><span style="color: lime">sys</span><span style="color: gray">.</span><span style="color: lime">columns </span><span style="color: teal">c  </span><span style="color: blue">on  </span><span style="color: teal">c</span><span style="color: gray">.</span><span style="color: magenta">object_id </span><span style="color: gray">= </span><span style="color: teal">parent_object_id
                                              </span><span style="color: gray">and </span><span style="color: teal">c</span><span style="color: gray">.</span><span style="color: teal">column_id </span><span style="color: gray">= </span><span style="color: teal">fc</span><span style="color: gray">.</span><span style="color: teal">parent_column_id
                    </span><span style="color: blue">where </span><span style="color: teal">fc</span><span style="color: gray">.</span><span style="color: teal">parent_object_id </span><span style="color: gray">= </span><span style="color: teal">@tabelObjectId </span><span style="color: gray">and </span><span style="color: teal">c</span><span style="color: gray">.</span><span style="color: teal">name </span><span style="color: gray">= </span><span style="color: teal">ac</span><span style="color: gray">.</span><span style="color: teal">name
                  </span><span style="color: gray">) </span><span style="color: blue">then </span><span style="color: red">'Yes' </span><span style="color: blue">else </span><span style="color: red">'No' </span><span style="color: blue">end
from </span><span style="color: lime">sys</span><span style="color: gray">.</span><span style="color: lime">all_columns </span><span style="color: teal">ac </span><span style="color: blue">where </span><span style="color: teal">ac</span><span style="color: gray">.</span><span style="color: magenta">object_id </span><span style="color: gray">= </span><span style="color: teal">@tabelObjectId
</span></pre>

<p><strong>Result for a table</strong></p>

<p>&#160;</p>

<table style="text-align: left; line-height: normal; border-collapse: collapse" border="0" cellspacing="0" cellpadding="0" width="482"><colgroup><col style="width: 74pt; mso-width-source: userset; mso-width-alt: 3584" width="98" /><col style="width: 48pt" span="span" width="64" /></colgroup><tbody>
    <tr style="height: 15pt" height="20">
      <td style="border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: #d9d9d9; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: windowtext 0.5pt solid; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl65" height="20" width="98"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Column_name</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: #d9d9d9; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: windowtext 0.5pt solid; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl65" width="64"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Type</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: #d9d9d9; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: windowtext 0.5pt solid; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl65" width="64"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Length</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: #d9d9d9; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: windowtext 0.5pt solid; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl65" width="64"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Nullable</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: #d9d9d9; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: windowtext 0.5pt solid; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl65" width="64"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Identity</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: #d9d9d9; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: windowtext 0.5pt solid; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl65" width="64"><font face="Calibri"><font style="font-size: 11pt" color="#000000">PK</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: #d9d9d9; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: windowtext 0.5pt solid; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl65" width="64"><font face="Calibri"><font style="font-size: 11pt" color="#000000">FK</font></font></td>
    </tr>

    <tr style="height: 15pt" height="20">
      <td style="border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67" height="20"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Id</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">int</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">4</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Yes</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Yes</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>
    </tr>

    <tr style="height: 15pt" height="20">
      <td style="border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67" height="20"><font face="Calibri"><font style="font-size: 11pt" color="#000000">AddressId</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">int</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">4</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Yes</font></font></td>
    </tr>

    <tr style="height: 15pt" height="20">
      <td style="border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67" height="20"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Weekday</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">smallint</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">2</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>
    </tr>

    <tr style="height: 15pt" height="20">
      <td style="border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67" height="20"><font face="Calibri"><font style="font-size: 11pt" color="#000000">From</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">time</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">5</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Yes</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>
    </tr>

    <tr style="height: 15pt" height="20">
      <td style="border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67" height="20"><font face="Calibri"><font style="font-size: 11pt" color="#000000">To</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">time</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">5</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Yes</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>
    </tr>

    <tr style="height: 15pt" height="20">
      <td style="border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67" height="20"><font face="Calibri"><font style="font-size: 11pt" color="#000000">ResetDate</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">date</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">3</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">Yes</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>

      <td style="border-bottom: windowtext 0.5pt solid; border-left: medium none; padding-left: 1px; padding-right: 1px; vertical-align: bottom; border-top: medium none; border-right: windowtext 0.5pt solid; padding-top: 1px" class="xl67"><font face="Calibri"><font style="font-size: 11pt" color="#000000">No</font></font></td>
    </tr>
  </tbody></table>