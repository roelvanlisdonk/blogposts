---
ID: 1419
post_title: Unit testing SSIS 2008 expressions
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/05/21/unit-testing-ssis-2008-expressions/
published: true
post_date: 2010-05-21 10:18:37
---
<p align="left">In Microsoft SQL Server 2008 Integration Services, you can use expressions, see (Integration Services Expression Concepts, <a title="http://technet.microsoft.com/en-us/library/ms141827.aspx" href="http://technet.microsoft.com/en-us/library/ms141827.aspx">http://technet.microsoft.com/en-us/library/ms141827.aspx</a>) in your dataflow tasks. </p>  <p align="left">For instance, if you want to import a flat file containing 2 columns: FirstName and LastName and your destination table contains only one column: Name, then you can concatenate the two columns by using a SSIS expression: @FirstName + @LastName, this is a very simple example, but when you are creating larger expressions like:    <br />    <br /><font color="#408080" size="1">((DATEDIFF(&quot;ss&quot;,(DT_DBTIMESTAMP)(SUBSTRING(DatumVoormelding,5,2) + &quot;/&quot; + SUBSTRING(DatumVoormelding,7,2) + &quot;/&quot; + SUBSTRING(DatumVoormelding,1,4) + &quot; &quot; + SUBSTRING(TijdstipVoormelding,1,2) + &quot;:&quot; + SUBSTRING(TijdstipVoormelding,3,2) + &quot;:&quot; + SUBSTRING(TijdstipVoormelding,5,2)),(DT_DBTIMESTAMP)(SUBSTRING(DatumSorteerbeslissing,5,2) + &quot;/&quot; + SUBSTRING(DatumSorteerbeslissing,7,2) + &quot;/&quot; + SUBSTRING(DatumSorteerbeslissing,1,4) + &quot; &quot; + SUBSTRING(TijdstipSorteerbeslissing,1,2) + &quot;:&quot; + SUBSTRING(TijdstipSorteerbeslissing,3,2) + &quot;:&quot; + SUBSTRING(TijdstipSorteerbeslissing,5,2)))) &gt; @[User::MinTijdsduurVoorgemeld]) ? 1 : 0      <br /></font>    <br />things can get more complicated and then you might want to use a unit test, to test this specific expression.     <br />    <br />    <br />There are several ways to unit test, a SSIS expression:</p>  <ul>   <li>     <div align="left">Using C# and the SSIS object model: <a title="http://www.codeproject.com/KB/database/Digging_SSIS_object_model.aspx" href="http://www.codeproject.com/KB/database/Digging_SSIS_object_model.aspx">http://www.codeproject.com/KB/database/Digging_SSIS_object_model.aspx</a></div>   </li>    <li>     <div align="left">Converting the SSIS expression to a SSIS Script Task, some calculation can’t be done with SSIS expressions, then you can use a SSIS Script task, this task can be written in C# and the C# code can be unit tested in Visual Studio.</div>   </li>    <li>     <div align="left">Adding a second SSIS project to your solution, that contains SSIS dataflow task for every unit test</div>   </li> </ul>  <p align="left">If you just want to manually test the expression without running the complete package, you can create a second SSIS Project to your solution and use flat file source, destination and dataflow tasks to unit test only the SSIS expression. In the screen dumps I added a second SSIS project named: <strong>Tpp.Miss.Etl.UnitTest</strong></p>  <p align="left">&#160;</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image62.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb61.png" width="354" height="507" /></a>     <br /></p>  <p align="left"><strong>UnitTest_Voorgemeld_Input.txt      <br /></strong>The UnitTest_Voorgemeld_Input.txt contains all the input data needed to unit test the SSIS expression:     <br />20100521,083030,20100521,084030     <br />20100521,,20100521,084030     <br />20100521,083030,20100521,</p>  <p align="left">&#160;</p>  <p align="left"><strong>Data flow task</strong>     <br />The data flow task contains:</p>  <ul>   <li>     <div align="left">Flat File Source (UnitTest_Voorgemeld_Input)</div>   </li>    <li>     <div align="left">Derived Column (contains the SSIS expression)</div>   </li>    <li>     <div align="left">Flat File Destination (UnitTest_Voorgemeld_Output)</div>   </li> </ul>  <p align="left">&#160;</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image63.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb62.png" width="754" height="514" /></a>     <br />    <br /><strong>Flat File Source</strong></p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image64.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb63.png" width="504" height="493" /></a> </p>  <p align="left">&#160;</p>  <p align="left"><strong>Derived Column (contains the SSIS expression)</strong></p>  <p align="left">Because the Derived column is “Added as a new column”, we must add this new column to the output flat file connection and map the derived column to the output column, to store the expression result in the unit test output file.</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image65.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb64.png" width="504" height="354" /></a> </p>  <p align="left"><strong>Flat File Destination</strong></p>  <p align="left">The flat file destination, contains one extra column: Voorgemeld</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image66.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb65.png" width="504" height="521" /></a> </p>  <p align="left">Extra column must be mapped:</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image67.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb66.png" width="504" height="502" /></a> </p>  <p align="left">&#160;</p>  <p align="left">&#160;</p>  <p align="left"><strong>UnitTest_Voorgemeld_Output.txt</strong></p>  <p align="left">The UnitTest_Voorgemeld_Output.txt contains all the unit test output, after running the unit test package the result will be:</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image68.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb67.png" width="754" height="423" /></a> </p>  <p align="left">In the file UnitTest_Voorgemeld_Output.txt:    <br />20100521,083030,20100521,084030,20100521083030     <br />20100521,,20100521,084030,20100521     <br />20100521,083030,20100521,,20100521083030</p>  <p align="left">&#160;</p>  <p align="left">By storing the unit test data en the unit test package in the same solution as the SSIS project that uses the expression, our continuous integration server can run the complete packages and the individual unit tests in the nightly builds.</p>  <p align="left">&#160;</p>  <p align="left">&#160;</p>  <p align="left">&#160;</p>  <p align="left">&#160;</p>  <p align="left">&#160;</p>  <p align="left">   <br /></p>  <p align="left">   <br /></p>  <p align="left"></p>