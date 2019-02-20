---
ID: 2034
post_title: >
  Using the sysdtslog90 table for logging
  package (user) variables in Microsoft
  SQL Server 2005 Integration Services
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/12/using-the-sysdtslog90-table-for-logging-package-user-variables-in-microsoft-sql-server-2005-integration-services/
published: true
post_date: 2011-05-12 11:44:12
---
<p>The sysdtslog90 table is used by Microsoft SQL Server 2005 SSIS to log messages. If you want to use this table for custom logging, you can user event handlers on SSIS tasks. </p> <p>- Select the task that uses a package variable</p> <p>- Click on the tab [Event Handlers]</p> <p>- Select [OnPreExecute], if you want to log the value of the parameter before the task is executed.</p> <p>- Select [OnPostExecute], if you want to log the value of the parameter after the task is executed.</p> <p>- Add a SQL Task from the Toolbox (control flow items)</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image7.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb7.png" width="580" height="220"></a></p> <p>- Use the following parameter mappings (the User::FileOutputPath is the package variable I want to log):</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image8.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb8.png" width="563" height="400"></a></p> <p>- Use as query:</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image9.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb9.png" width="556" height="535"></a><pre class="code"><span style="color: green">-- Determine current date and time
</span><span style="color: blue">declare @now datetime
select @now </span><span style="color: gray">= </span><span style="color: magenta">getdate</span><span style="color: gray">()

</span><span style="color: blue">declare @up1 nvarchar</span><span style="color: gray">(128)
</span><span style="color: blue">declare @up2 nvarchar</span><span style="color: gray">(128)
</span><span style="color: blue">declare @up3 nvarchar</span><span style="color: gray">(128)
</span><span style="color: blue">declare @up4 nvarchar</span><span style="color: gray">(128)
</span><span style="color: blue">declare @up5 nvarchar</span><span style="color: gray">(128)
</span><span style="color: blue">set @up1 </span><span style="color: gray">= ?
</span><span style="color: blue">set @up2 </span><span style="color: gray">= ?
</span><span style="color: blue">set @up3 </span><span style="color: gray">= ?
</span><span style="color: blue">set @up4 </span><span style="color: gray">= ?
</span><span style="color: blue">set @up5 </span><span style="color: gray">= ?

</span><span style="color: blue">declare @message nvarchar</span><span style="color: gray">(2048)
</span><span style="color: blue">set @message </span><span style="color: gray">= </span><span style="color: red">'FileOutputPath=[' </span><span style="color: gray">+ </span><span style="color: magenta">isnull</span><span style="color: gray">(?, </span><span style="color: red">' '</span><span style="color: gray">) + </span><span style="color: red">']'

</span><span style="color: green">-- Add a record to the table [ZKP_Audit].[dbo].[sysdtslog90]
</span><span style="color: blue">exec sp_dts_addlogentry 

</span><span style="color: red">'OnPreExecute'</span><span style="color: gray">,                </span><span style="color: green">-- [event]:        Eventname

@up1</span><span style="color: gray">,                    </span><span style="color: green">-- [computer]:    Machinename

@up2</span><span style="color: gray">,                    </span><span style="color: green">-- [operator]:    Username

@up3</span><span style="color: gray">,                    </span><span style="color: green">-- [source]:    Taskname

@up4</span><span style="color: gray">,                    </span><span style="color: green">-- [sourceid]:    Task GUID

@up5</span><span style="color: gray">,                    </span><span style="color: green">-- [executionid]:    Package GUID

@now</span><span style="color: gray">,                    </span><span style="color: green">-- [starttime]:    Current date and time

@now</span><span style="color: gray">,                    </span><span style="color: green">-- [endtime]:    Current date and time

0</span><span style="color: gray">,                    </span><span style="color: green">-- [datacode]:    Not used, always 0

0x</span><span style="color: gray">,                    </span><span style="color: green">-- [databytes]:    Not used, always 0x

@message                 -- [message]:    Message containing te parameterinformation
</pre></span></p>
<h2>Result in the table sysdtslog90:</h2>
<p>&nbsp;</p>
<p>14&nbsp;&nbsp;&nbsp; 14&nbsp;&nbsp;&nbsp; OnPreExecute&nbsp;&nbsp;&nbsp; DEV2005&nbsp;&nbsp;&nbsp; DEV2005\Administrator&nbsp;&nbsp;&nbsp; Log package variables&nbsp;&nbsp;&nbsp; 5325CAAB-AC92-456E-B206-8DF8DA4081A8&nbsp;&nbsp;&nbsp; 013DC323-7A0D-48FC-BAA0-07074FC765EE&nbsp;&nbsp;&nbsp; 2011-05-12 11:28:44.947&nbsp;&nbsp;&nbsp; 2011-05-12 11:28:44.947&nbsp;&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp; 0x&nbsp;&nbsp;&nbsp; FileOutputPath=[C:\Projects\De Grote Rivieren\Dagstaten\Solution\SSIS\ZKP_Dagstaten2Psygis\Files\Export\]</p>