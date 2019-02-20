---
ID: 314
post_title: >
  When the Microsoft SQL Server Import and
  Export wizard is not enough
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/30/when-the-microsoft-sql-server-import-and-export-wizard-is-not-enough/
published: true
post_date: 2009-03-30 13:04:19
---
<p>When importing data from Microsoft Access to Microsoft SQL Server you can use the Microsoft SQL Server Import and Export wizard, but some times you can not use this wizard because values in a column can't be casted to the correct format.</p> <p>&nbsp;</p> <p>Like a "Series" column that contains the values (1,2,3 and a ' ') to a int column. To quickly import the data, I created a temp table, with the exact same columns accept for the "Series" column. Edit the mappings and source table in the import and export wizard.</p> <p>&nbsp;</p> <p><a href="http://roelvanlisdonk.files.wordpress.com/2009/03/image5.png"><img style="border-bottom:0;border-left:0;border-top:0;border-right:0;" border="0" alt="image" src="http://roelvanlisdonk.files.wordpress.com/2009/03/image-thumb5.png" width="335" height="270"></a> </p> <p>&nbsp;</p><pre class="code"><span style="color:blue;">insert into </span>Postcode <span style="color:gray;">(</span>Postcode<span style="color:gray;">, </span>Straatnaam<span style="color:gray;">, </span>Plaats<span style="color:gray;">, </span>RangeStart<span style="color:gray;">, </span>RangeEind<span style="color:gray;">, </span>PostcodetypeId<span style="color:gray;">)
</span><span style="color:blue;">select distinct </span>pt<span style="color:gray;">.</span>Postcode<span style="color:gray;">, </span>pt<span style="color:gray;">.</span>Straatnaam<span style="color:gray;">, </span>pt<span style="color:gray;">.</span>Plaats<span style="color:gray;">, </span>pt<span style="color:gray;">.</span>RangeStart<span style="color:gray;">, </span>pt<span style="color:gray;">.</span>RangeEind<span style="color:gray;">,
</span><span style="color:magenta;">cast</span><span style="color:gray;">(
    </span><span style="color:blue;">case
        when </span>pt<span style="color:gray;">.</span>PostcodetypeId <span style="color:gray;">= </span><span style="color:red;">' ' </span><span style="color:blue;">then </span><span style="color:gray;">-</span>1
        <span style="color:blue;">when </span>pt<span style="color:gray;">.</span>PostcodetypeId <span style="color:gray;">is null </span><span style="color:blue;">then </span><span style="color:gray;">-</span>1
        <span style="color:blue;">when </span>pt<span style="color:gray;">.</span>PostcodetypeId <span style="color:gray;">= </span><span style="color:red;">'' </span><span style="color:blue;">then </span><span style="color:gray;">-</span>1
        <span style="color:blue;">else </span>pt<span style="color:gray;">.</span>PostcodetypeId
    <span style="color:blue;">end
as int</span><span style="color:gray;">)
</span><span style="color:blue;">from </span>PostcodeTemp pt</pre><a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>