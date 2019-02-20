---
ID: 732
post_title: Using TSQL Like operator in LLBLGen
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/02/using-tsql-like-operator-in-llblgen/
published: true
post_date: 2009-10-02 09:46:45
---
<p>If you want to query you’re database with LLBLGen, by filtering entities using the TQL Like operator you should use the FieldLikePredicate   <br />    <br />    <br />See LLGLGen v2.6 documentation: <a title="http://www.llblgen.com/documentation/2.6/hh_start.htm" href="http://www.llblgen.com/documentation/2.6/hh_start.htm">http://www.llblgen.com/documentation/2.6/hh_start.htm</a>    <br />Specific part: <a title="http://www.llblgen.com/documentation/2.6/Using%20the%20generated%20code/Adapter/Filtering%20and%20Sorting/gencode_filteringpredicateclasses_adapter.htm#FieldLikePredicate" href="http://www.llblgen.com/documentation/2.6/Using%20the%20generated%20code/Adapter/Filtering%20and%20Sorting/gencode_filteringpredicateclasses_adapter.htm#FieldLikePredicate">http://www.llblgen.com/documentation/2.6/Using%20the%20generated%20code/Adapter/Filtering%20and%20Sorting/gencode_filteringpredicateclasses_adapter.htm#FieldLikePredicate</a>    <br />    <br />    <br /></p>  <p><strong><font size="4">FieldLikePredicate</font></strong></p>  <p><b>Description</b>    <br />compares the entity field specified with the pattern specified, using the LIKE operator. The pattern should contain the wildcard, which is '%' (also for MS Access). FieldLikePredicate performs a LIKE compare using the case sensitivity setting of the database system the query is executed on: the SQL generated does not contain any collation information nor any case insensitive setting if the database is using case sensitive comparison operations by default (Oracle, some SqlServer installations). You can perform case insensitive compares however, if the database is case sensitive, by setting the <b>CaseSensitiveCollation</b> property to true prior to passing the predicate to a fetch method like FetchEntityCollection(). This will perform the UPPERCASE variant of the field with the pattern specified.Please note that if you've set CaseSensitiveCollaction to true, you've to specify your pattern in uppercase as well.</p>  <p><b>SQL equivalent examples</b>    <br />Field LIKE '%bla'    <br />Field LIKE 'bla%'</p>  <p><b>Operators</b>    <br />none.</p>  <p><b>Example</b>    <br />This example creates a predicate which compares Customer.CompanyName to the pattern &quot;Solution%&quot;.</p>  <ul>   <li>C# </li>    <li>VB.NET </li> </ul>  <pre>// C#
filter.Add(new FieldLikePredicate(CustomerFields.CompanyName, null, &quot;Solution%&quot;));

// Which is equal to:
filter.Add(CustomerFields.CompanyName % &quot;Solution%&quot;);</pre>

<pre>' VB.NET
filter.Add(New FieldLikePredicate(CustomerFields.CompanyName, Nothing, &quot;Solution%&quot;))

' Which is equal to: (VB.NET 2005)
filter.Add(CustomerFields.CompanyName Mod &quot;Solution%&quot;)</pre>

<p>Note, that the operator syntaxis is a little odd in VB.NET, due to the fact that there isn't an ability to add new operators to VB.NET/C#. </p>

<p><b>Can be used for in-memory filtering</b>

  <br />Yes. When used in in-memory filters, the pattern can either be a normal LIKE statement pattern with '%' wildcards, or it can be a full regular expression. If the pattern is a regular expression, be sure to set the property <b>PatternIsRegEx</b> to true. See also the LLBLGen Pro reference manual on more detailed information about the properties of the FieldLikePredicate</p>