---
ID: 427
post_title: 'Microsoft SQL 2005 Bulk Insert &#8211; Kerberos double hop &#8211; and Operating system error code 5 (Access is denied)'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/microsoft-sql-2005-bulk-insert-kerberos-double-hop-and-operating-system-error-code-5-access-is-denied/
published: true
post_date: 2009-05-22 09:00:18
---
<div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClassBD6EEBF93B3A4383945497223AE9EF34">         <p></p>          <p><span style="color: #88ac0b; font-size: 16pt"><strong>Description </strong></span></p>          <p>Microsoft SQL 2005 Bulk Insert &#8211; Kerberos double hop - and Operating system error code 5 (Access is denied)           <br />After upgrading Microsoft SQL Server 2000 SP4 to Microsoft SQL 2005 SP2, a stored procedure with             <br />a bulk insert statement, started to throw an error.            <br /></p>          <p><span style="color: #88ac0b; font-size: 16pt"><strong>Error </strong></span></p>          <p><span style="font-family: cambria"><span style="color: black">Cannot bulk load because the file &quot;<a></a></span>\\ServerA\NetworkShare\Import\20080315.csv<span style="color: black">&quot; could not be opened. Operating system error code 5(Access is denied.).               <br /></span></span></p>          <p><span style="color: #88ac0b; font-size: 16pt"><strong>TSQL</strong></span> </p>          <p>The t-sql code that caused the problem:           <br />declare @ImportFile as varchar(255)            <br />set @ImportFile = '<a><span style="font-family: cambria">\\ServerA\NetworkShare\Import\20080315.csv</span></a>'            <br />exec ('bulk insert dbo.ImportTable from ''' + @ImportFile + ''' WITH (FIELDTERMINATOR = '','', ROWTERMINATOR = ''\n'')')            <br /></p>          <p><span style="color: #88ac0b; font-size: 16pt"><strong>Infrastructure </strong></span></p>          <p>To understand the error, you must first understand the environment infrastructure.           <br />            <br /><strong>ServerA             <br /></strong></p>          <div>           <table style="border-collapse: collapse" border="0"><colgroup><col style="width: 638px" /></colgroup><tbody valign="top">               <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: black 0.5pt solid; border-right: black 0.5pt solid">                   <p>Microsoft Windows Server 2003 Standard SP1</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Server is member of an OU with the High Secure Template C:\WINDOWS\security\templates\ hisecws.inf applied to it.</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Server contains a custom made .NET 2.0 WindowsService with Identity DOMAIN\srvaWindowService</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>.NET 2.0 WindowsService has a database connectionstring: &quot;Data Source=ServerB;Initial Catalog=DBTEST;Integrated Security=True; &quot;</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Server contains a Network Share '\\ServerA\NetworkShare\'</p>                 </td>               </tr>             </tbody></table>         </div>          <p>&#160;</p>          <p><strong>ServerB </strong></p>          <div>           <table style="border-collapse: collapse" border="0"><colgroup><col style="width: 638px" /></colgroup><tbody valign="top">               <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: black 0.5pt solid; border-right: black 0.5pt solid">                   <p>Microsoft Windows Server 2003 Standard SP1</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Microsoft SQL Server 2005 SP2</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Microsoft SQL Server 2005 named instance (ServerB\InstanceName) on static port 1433</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Microsoft SQL Server 2005: Only Shared Memory en TCP/IP enabled (Named Pipes are Disabled)</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Microsoft SQL Server 2005 Server authentication: Windows Authentication mode</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>The Microsoft SQL Server 2005 named instance identity is a Active Directory account DOMAIN\srvaSQLServer</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Microsoft SQL Server 2005 instance (ServerB\InstanceName) contains a database (DBTEST) with Compatibility level: SQL Server 2005 (90)</p>                 </td>               </tr>             </tbody></table>         </div>          <p>&#160;</p>          <p><strong>Active Directory Server </strong></p>          <div>           <table style="border-collapse: collapse" border="0"><colgroup><col style="width: 638px" /></colgroup><tbody valign="top">               <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: black 0.5pt solid; border-right: black 0.5pt solid">                   <p>Microsoft Windows Server 2003 Standard SP1</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Server is member of an OU with the High Secure Template C:\WINDOWS\security\templates\hisecdc.inf applied to it.</p>                 </td>               </tr>             </tbody></table>         </div>          <p>&#160;</p>          <p><strong>Accounts and Rights </strong></p>          <div>           <table style="border-collapse: collapse" border="0"><colgroup><col style="width: 638px" /></colgroup><tbody valign="top">               <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: black 0.5pt solid; border-right: black 0.5pt solid">                   <p>Active Directory account DOMAIN\srvaSQLServer is local admin on ServerB (<span style="color: #984806">causes a problem, see solution</span>)</p>
               </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Active Directory account DOMAIN\srvaSQLServer has no Service Principal Name for the MS SQL Service on port 1433(<span style="color: #984806">causes a problem, see solution</span>)</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Active Directory account DOMAIN\srvaSQLServer is not &quot;Trusted for Delegation&quot; (<span style="color: #984806">causes a problem, see solution</span>)</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Active Directory account DOMAIN\srvaSQLServer has &quot;log on as a service&quot; rights</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>The Active Directory account DOMAIN\srvaWindowService has modify rights to the networkshare '\\ServerA\NetworkShare\'</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>The Active Directory account DOMAIN\srvaWindowService has modify rights to the filesystem networkshare '\\ServerA\NetworkShare\'</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Active Directory account DOMAIN\srvaWindowService has &quot;log on as a service&quot; rights.</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>Active Directory account DOMAIN\srvaWindowService is mapped to a login (DOMAIN\srvaWindowService) on the Microsft SQL Server 2005 instance (ServerB\InstanceName)</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>The Microsoft SQL Server 2005 Login DOMAIN\srvaWindowService is member of the server role &quot;bulk admin&quot;</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>The Microsoft SQL Server 2005 Login DOMAIN\srvaWindowService is mapped to a DBTEST database user DOMAIN\srvaWindowService</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>The database user DOMAIN\srvaWindowService has db_datareader and db_datawriter rights on the database DBTEST.</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>ServerB is not trusted for delegation (<span style="color: #984806">causes a problem, see solution</span>)</p>                 </td>               </tr>             </tbody></table>         </div>          <p>&#160;</p>          <p><span style="color: #88ac0b; font-size: 16pt"><strong>Problem Cause </strong></span></p>          <p>A file on a network share on ServerA is processed by a .NET 2.0 Windows Service on Server A with Identity (DOMAIN\srvaWindowsService). During processing a stored procedure on Server B is called with parameter '<a><span style="font-family: cambria">\\ServerA\NetworkShare\Import\20080315.csv</span></a>' with Windows Integrated Security. The stored procedure tries to bulk inserts the data in the database. In SQL Server 2000 this processing will succeed, because SQL Server 2000 will automaticly delegate the call to the network share on behave of the Active Directory account (DOMAIN\srvaWindowsService), so the call succeeds. Microsoft considered this a security hole and Microsoft SQL Server 2005 will not automaticly delegate control. </p>          <p><em>Rich Baumet, explains on a MSDN forum             <br /></em>If you were to execute the statement on the SQL Server itself then it will work. If you were to move the file locally to the SQL Server this will work. Both will work because you are no longer doing a <span style="color: #984806">double hop</span> to execute and get the file. </p>          <p>&#160;</p>          <p><span style="color: #88ac0b; font-size: 16pt"><strong>Solution </strong></span></p>          <p>After following the steps on the MSDN Forum <a href="http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=928173&amp;SiteID=1">http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=928173&amp;SiteID=1</a> it still did not work.            <br />This problem was, that after restarting the Microsoft SQL Server 2005 instance service, the SPN disappeared from active directory. After some testing we found the solution that worked for us.             <br />Add the Active Directory account DOMAIN\srvaSQLServer to the domain admin group.            <br />Restart the Microsoft SQL Server 2005 instance service.             <br />            <br />After restarting the service you should see a new Service Principal Name in Active directory:            <br />In the Microsft Windows 2003 support tools, you can found the executable setspn.exe            <br />Execute setspn -L DOMAIN\srvaSQLServer             <br />            <br />Registered ServicePrincipalNames for CN=srvaSQLServer,OU=Users,DC=domain,DC=corp:            <br /><span style="color: black">MSSQLSvc/ServerB.domain.corp:1433</span>            <br />            <br />Follow the step 4 on the MSDN Forum            <br />(Now that we created the SPN for the SQL Service we must allow it to delegate. Using Active Directory Users and Computers go to the properties of the account the SQL Service is running under.There should be a DELEGATION tab there On the Delegation tab select &quot;Trust this user for delegation to any service (Kerberos only)            <br />            <br />This step must be repeated for ServerB (go to active directory, select server ServerB, go to the tab delegation and select &quot;Trust this user for delegation to any service (Kerberos only)            <br />            <br /><strong>After following this steps it still did not work!!!             <br /></strong>This was caused by the caching of the Keberos tickets. During the bulk insert error the ServerA en ServerB, got a Keberos tickets that denied access to the network share. These tickets are cached. Clear the caching (purchase tickets) with the kerbtray.exe tool found in de the Microsft Windows 2003 Resource Kit </p>          <p>&#160;</p>          <p><span style="color: #88ac0b; font-size: 16pt"><strong>Additional Information</stro
ng></span>            <br /></p>          <div>           <table style="border-collapse: collapse" border="0"><colgroup><col style="width: 215px" /><col style="width: 423px" /></colgroup><tbody valign="top">               <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: black 0.5pt solid; border-right: black 0.5pt solid">                   <p>MSDN Forum</p>                 </td>                  <td style="border-bottom: black 0.5pt solid; border-left: medium none; padding-left: 7px; padding-right: 7px; border-top: black 0.5pt solid; border-right: black 0.5pt solid">                   <p><a href="http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=928173&amp;SiteID=1">http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=928173&amp;SiteID=1</a>                      <br />                      <br />This post started the solution for us, many tanks to Rich Baumet</p>                 </td>               </tr>                <tr>                 <td style="border-bottom: black 0.5pt solid; border-left: black 0.5pt solid; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p>MSDN Forum</p>                 </td>                  <td style="border-bottom: black 0.5pt solid; border-left: medium none; padding-left: 7px; padding-right: 7px; border-top: medium none; border-right: black 0.5pt solid">                   <p><a href="http://forums.microsoft.com/msdn/showpost.aspx?postid=107193&amp;siteid=1&amp;sb=0&amp;d=1&amp;at=7&amp;ft=11&amp;tf=0&amp;pageid=1">http://forums.microsoft.com/msdn/showpost.aspx?postid=107193&amp;siteid=1&amp;sb=0&amp;d=1&amp;at=7&amp;ft=11&amp;tf=0&amp;pageid=1</a>                      <br />                      <br />This form ends with: <span style="font-family: arial; color: black; font-size: 7pt">After watching forums, etc. for almost a year regarding this issue, we ran a MS Support Request. After several hours of walking them through the issue, they said it was definitely a bug ( # 396489 ) in 2005 and would be fixed in 2008.                       <br /></span><span style="color: #984806">In our situation it was not a bug in Microsoft SQL Server 2005 SP2, but a configuration error in Active Directory</span></p>                 </td>               </tr>             </tbody></table>         </div>          <p>&#160;</p>       </div>     </div>     <span class="blankline"></span></div> </div>