---
ID: 2051
post_title: >
  Scripting triggers in Microsoft SQL
  Server
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/17/scripting-triggers-in-microsoft-sql-server/
published: true
post_date: 2011-05-17 14:11:49
---
<p>By default when you use the Script Wizard in Microsoft SQL Server Management Studio to script objects in a database, triggers are note included.</p> <p>You can include triggers if you [Include all objects] and [Set triggers= true] during the Script Wizard.</p> <p>&nbsp;</p> <p>To start the script wizard, right click the database that contains the triggers.</p> <p>Choose Tasks &gt; Generate Scripts…</p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image11.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb11.png" width="546" height="462"></a></p> <p>&nbsp;</p> <p>Check the [Script all objects in the selected database]</p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image12.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb12.png" width="509" height="461"></a></p> <p>&nbsp;</p> <p>Set the [Script Triggers = True]</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image13.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb13.png" width="498" height="451"></a></p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image14.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb14.png" width="488" height="442"></a></p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image15.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb15.png" width="483" height="437"></a></p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image16.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb16.png" width="484" height="438"></a></p> <p>&nbsp;</p> <p>The generate script will now contain all triggers in the database.</p> <p>It will not generate drop statements for the triggers</p> <p>So you should at [drop trigger] if it exists, before executing the generated create trigger statements:</p> <p>For example the script wizard generates:</p><pre class="code"><span style="color: blue">CREATE TRIGGER [trd_Order] on [Order]
AFTER DELETE
AS

    INSERT Audit_Order
    SELECT </span><span style="color: gray">*, </span><span style="color: red">'V'</span><span style="color: gray">,0,</span><span style="color: magenta">getdate</span><span style="color: gray">()
    ,    null
    ,    null
     </span><span style="color: blue">FROM deleted
END
GO
</pre></span>
<p>Then you should change this to:</p>
<p><pre class="code"><span style="color: blue">IF </span><span style="color: magenta">OBJECT_ID </span><span style="color: gray">(</span><span style="color: red">'trd_Order'</span><span style="color: gray">, </span><span style="color: red">'TR'</span><span style="color: gray">) IS NOT NULL
</span><span style="color: blue">BEGIN
   DROP TRIGGER </span>trd_Order
<span style="color: blue">END

CREATE TRIGGER </span>[trd_Order] <span style="color: blue">on </span>[Order]
<span style="color: blue">AFTER DELETE
AS

    INSERT </span>Audit_Order
    <span style="color: blue">SELECT </span><span style="color: gray">*, </span><span style="color: red">'V'</span><span style="color: gray">,</span>0<span style="color: gray">,</span><span style="color: magenta">getdate</span><span style="color: gray">()
    ,    null
    ,    null
     </span><span style="color: blue">FROM </span>deleted
<span style="color: blue">END
</span>GO</pre></p>