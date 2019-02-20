---
ID: 3154
post_title: >
  Notes on SqlDependency and
  QueryNotification in Microsoft SQL
  Server 2012
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/02/01/notes-on-sqldependency-and-querynotification-in-microsoft-sql-server-2012/
published: true
post_date: 2013-02-01 09:47:22
---
<p>When you want to start using SqlDependency for QueryNotification in Microsoft SQL Server 2012, there are some steps you need to take, to make this work.</p>  <p>&#160;</p>  <h2>In development </h2>  <p>In development you should take the following steps:</p>  <p>&#160;</p>  <p><strong>Make &quot;sa&quot; dbo</strong></p>  <p>use [master]    <br />go     <br />alter authorization on database::[<font color="#8064a2">Your database name here</font>] to [sa]     <br />go</p>  <p>&#160;</p>  <p><strong>Client should connect as &quot;sa&quot;</strong></p>  <p>Use &quot;sa&quot; to connect to the database, when subscribing a query for QueryNotification</p>  <p>&#160;</p>  <p><strong>Check if SqlDependency is enabled on the database</strong></p>  <p>use [master]    <br />go     <br />select name, is_broker_enabled from sys.databases     <br />go</p>  <p>&#160;</p>  <p><strong>Enable SqlDependency on the database</strong></p>  <p>use [master]    <br />go     <br />alter database [<font color="#8064a2">Your database name here</font>] set enable_broker with rollback immediate     <br />go</p>  <p>To disable SqlDependency, see notes below.</p>  <p>&#160;</p>  <p><strong>Database SET OPTIONS</strong></p>  <p>For more information on the database SET OPTIONS, see the notes below</p>  <p>SET ANSI_NULLS ON    <br />SET ANSI_PADDING ON     <br />SET ANSI_WARNINGS ON     <br />SET CONCAT_NULL_YIELDS_NULL ON     <br />SET QUOTED_IDENTIFIER ON     <br />SET NUMERIC_ROUNDABORT OFF     <br />SET ARITHABORT ON</p>  <p>&#160;</p>  <p><strong>Stored procedure </strong></p>  <p>When using a stored procedure as query for the QueryNotification, make sure the database options above are set before the stored procedure is created:</p>  <p>&#160;</p>  <p>if object_id('Reporting.SqlDependency_GetProcesses') is not null    <br />begin     <br />&#160;&#160;&#160; drop procedure Reporting.SqlDependency_GetProcesses     <br />end     <br />go</p>  <p>SET ANSI_NULLS ON    <br />SET ANSI_PADDING ON     <br />SET ANSI_WARNINGS ON     <br />SET CONCAT_NULL_YIELDS_NULL ON     <br />SET QUOTED_IDENTIFIER ON     <br />SET NUMERIC_ROUNDABORT OFF     <br />SET ARITHABORT ON</p>  <p>create procedure Reporting.SqlDependency_GetProcesses    <br />as     <br />begin     <br />&#160;&#160;&#160; select&#160; Id,     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Name,     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; StartCheckTime,     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; EndCheckTime,     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; OranjeAlertTime,     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; RedAlertTime,     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; LastImportDateTime,     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; StatusId     <br />&#160;&#160;&#160; from&#160;&#160;&#160; General.Proces     <br />end     <br />go</p>  <p>&#160;</p>  <p><font color="#800000">DO NOT ADD with(nolock)</font>, because database isolation level <strong>read uncommitted</strong> is not allowed in queries that are used in the QueryNotification subscription.</p>  <p>&#160;</p>  <h2>C# code</h2>  <p><strong></strong></p>  <p><strong>Always re-register for QueryNotification, in the SqlDependency OnChange eventhandler</strong>.</p>  <p>The object containing the SqlDependency OnChange eventhandler, should be alive, in other words, when you are using SqlDependency in a WebApi or MVC 4 controler, save the object containing the SqlDependency OnChange eventhandler between request aka make it static <img class="wlEmoticon wlEmoticon-winkingsmile" style="border-top-style: none; border-left-style: none; border-bottom-style: none; border-right-style: none" alt="Winking smile" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/wlEmoticon-winkingsmile.png" /></p>  <p>&#160;</p>  <p><strong>Use Schema.StoredProcedureName, in the registration call</strong></p>  <p>&#160;</p>  <p>Some example code for registring a stored procedure for QueryNotification:</p>  <pre class="code"><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Process
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">Id { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Name { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">TimeSpan </span><span style="background: white; color: black">StartCheckTime { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">TimeSpan </span><span style="background: white; color: black">EndCheckTime { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">TimeSpan </span><span style="background: white; color: black">OrangeAlertTime { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">TimeSpan </span><span style="background: white; color: black">RedAlertTime { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">DateTime </span><span style="background: white; color: black">LastImportDateTime { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }</span><span style="background: white; color: gray">
        </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">StatusId { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }</span></pre>

<p>&#160;</p>

<pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Configuration;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Data.SqlClient;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Web;</span></pre>

<pre class="code"><span style="background: white; color: blue">private </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Process</span><span style="background: white; color: black">&gt; _data = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;</span></pre>

<p>&#160;</p>

<pre class="code"><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Refreshes the cached data.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">RefreshData()
        {
            </span><span style="background: white; color: blue">try
            </span><span style="background: white; color: black">{
                </span><span style="background: white; color: green">// To prevent errors, when database connection is lost, always stop SqlDependency subscription, before starting one.
                </span><span style="background: white; color: #2b91af">SqlDependency</span><span style="background: white; color: black">.Stop(</span><span style="background: white; color: #2b91af">ConfigurationManager</span><span style="background: white; color: black">.ConnectionStrings[</span><span style="background: white; color: #a31515">&quot;DefaultConnection&quot;</span><span style="background: white; color: black">].ConnectionString);
                </span><span style="background: white; color: #2b91af">SqlDependency</span><span style="background: white; color: black">.Start(</span><span style="background: white; color: #2b91af">ConfigurationManager</span><span style="background: white; color: black">.ConnectionStrings[</span><span style="background: white; color: #a31515">&quot;DefaultConnection&quot;</span><span style="background: white; color: black">].ConnectionString);

                </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">connection = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">SqlConnection</span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">ConfigurationManager</span><span style="background: white; color: black">.ConnectionStrings[</span><span style="background: white; color: #a31515">&quot;DefaultConnection&quot;</span><span style="background: white; color: black">].ConnectionString))
                {
                    </span><span style="background: white; color: green">// Define query.
                    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">storedProcedureName = </span><span style="background: white; color: #a31515">&quot;Reporting.SqlDependency_GetProcesses&quot;</span><span style="background: white; color: black">;

                    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">SqlCommand </span><span style="background: white; color: black">command = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">SqlCommand</span><span style="background: white; color: black">(storedProcedureName, connection))
                    {
                        command.CommandType = System.Data.</span><span style="background: white; color: #2b91af">CommandType</span><span style="background: white; color: black">.StoredProcedure;

                        </span><span style="background: white; color: green">// Make sure the command object does not already have a notification object associated with it.
                        </span><span style="background: white; color: black">command.Notification = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;

                        </span><span style="background: white; color: green">// Hookup sqldependency eventlistener (re-register for change events).
                        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dependency = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">SqlDependency</span><span style="background: white; color: black">(command);
                        dependency.OnChange += </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">OnChangeEventHandler</span><span style="background: white; color: black">(dependency_OnChange);

                        </span><span style="background: white; color: green">// Open connection to database.
                        </span><span style="background: white; color: black">connection.Open();

                        </span><span style="background: white; color: green">// Get the data from the database and convert to a list of DTO's.
                        </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">SqlDataReader </span><span style="background: white; color: black">reader = command.ExecuteReader())
                        {
                            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(reader.HasRows)
                            {
                                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">data = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;Process&gt;();
                                </span><span style="background: white; color: blue">while </span><span style="background: white; color: black">(reader.Read())
                                {
                                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">da = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Process
                                    {
                                        Id = reader.GetInt32(0),
                                        Name = reader.GetString(1),
                                        StartCheckTime = reader.GetTimeSpan(2),
                                        EndCheckTime = reader.GetTimeSpan(3),
                                        OrangeAlertTime = reader.GetTimeSpan(4),
                                        RedAlertTime = reader.GetTimeSpan(5),
                                        LastImportDateTime = reader.GetDateTime(6),
                                        StatusId = reader.GetInt32(7)
                                    };
                                    data.Add(da);
                                }

                                _data = data;
                            }
                        }
                    }
                }
            }
            </span><span style="background: white; color: blue">catch </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Exception </span><span style="background: white; color: black">ex)
            {
                _logger.Error(</span><span style="background: white; color: #a31515">&quot;Error.&quot;</span><span style="background: white; color: black">, ex);

                </span><span style="background: white; color: green">// Exception can be caused by a database connection los, so try to hookup sqldependency eventlistener again.
                </span><span style="background: white; color: black">RefreshData();
            }
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Fires, when the data in the database changes.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">private void </span><span style="background: white; color: black">dependency_OnChange(</span><span style="background: white; color: blue">object </span><span style="background: white; color: black">sender, </span><span style="background: white; color: #2b91af">SqlNotificationEventArgs </span><span style="background: white; color: black">e)
        {
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(e.Type == </span><span style="background: white; color: #2b91af">SqlNotificationType</span><span style="background: white; color: black">.Change)
            {
                </span><span style="background: white; color: green">// Re-register for query notification SqlDependency Change events.
                </span><span style="background: white; color: black">RefreshData();
            }
        }</span></pre>


<p><strong>In test</strong></p>

<p>When everything is working in development and you are shifting to the test environment, harden the security:</p>

<p><strong>Rights for DBO</strong></p>

<p>Do not make sa dbo owner, use a specific service account login [DOMAIN\ServiceAccountUsername].</p>

<p>&#160;</p>

<p><strong>Rights for client</strong></p>

<p align="left">Do not connect with SQL authentication, use windows authentication and connect with a specific client account login[DOMAIN\ClientAccountUsername].</p>

<p>grant subscribe query notifications to [You client login]</p>

<p>go</p>

<p align="left">&#160;</p>

<p align="left">&#160;</p>

<h1 align="left">NOTES</h1>

<p align="left"><strong></strong></p>

<p align="left"><strong>To disable SqlDependency on the database</strong></p>

<p align="left">use [master] 
  <br />

  <br />go</p>

<p align="left">alter database [<font color="#8064a2">Your database name here</font>] set disable_broker with rollback immediate</p>

<p align="left">go</p>

<p align="left">&#160;</p>

<p align="left"><strong>Trouble shooting</strong></p>

<p align="left">When SqlDependency does not fire events, start a standard Microsoft SQL Server profiler trace:</p>

<p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image_thumb.png" width="580" height="376" /></a></p>

<p align="left">&#160;</p>

<p align="left">Add the following specific events:</p>

<p align="left">- Enable all Broker events</p>

<p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image1.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image_thumb1.png" width="497" height="322" /></a></p>

<p align="left">- Enable all Query Notification</p>

<p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image2.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image_thumb2.png" width="500" height="320" /></a></p>

<p align="left">- Enable all Security Audit events</p>

<p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image3.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image_thumb3.png" width="511" height="329" /></a></p>

<p align="left">&#160;</p>

<p align="left"><strong>Correct subscriptions</strong></p>

<p align="left">Generate a record in the view sys.dm_qn_subscriptions</p>

<div align="left">
  <pre class="code"><span style="color: blue">select </span><span style="color: gray">* </span><span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">dm_qn_subscriptions
</span></pre>
</div>

<p align="left">&#160;</p>

<p align="left"><strong>Incorrect subscriptions</strong></p>

<p align="left">Incorrect QueryNotification subscriptions records contain:</p>

<p align="left">type=&quot;subscribe&quot; source=&quot;statement&quot; info=&quot;set options&quot; database_id=&quot;0&quot;</p>

<p align="left">where the INFO part contains a indication to the problem.</p>

<p align="left">&#160;</p>

<h2 align="left">Database SET OPTIONS</h2>

<p align="left">&#160;</p>

<p align="left"><strong>SET ANSI_NULLS <font color="#004000">ON</font></strong></p>

<p align="left"><a href="http://msdn.microsoft.com/en-us/library/ms188048.aspx">http://msdn.microsoft.com/en-us/library/ms188048.aspx</a></p>

<ul>
  <li>
    <div align="left">In a future version of Microsoft SQL Server ANSI_PADDING will always be ON and any applications that explicitly set the option to OFF will produce an error. </div>
  </li>

  <li>
    <div align="left">When SET ANSI_NULLS is ON, you can't compare NULL values with the = or &lt;&gt; operators and you should use the IS operator. </div>
  </li>
</ul>

<p align="left"><strong>SET ANSI_PADDING <font color="#004000">ON</font></strong></p>

<p align="left"><a href="http://msdn.microsoft.com/en-us/library/ms187403.aspx">http://msdn.microsoft.com/en-us/library/ms187403.aspx</a></p>

<ul>
  <li>
    <div align="left">In a future version of Microsoft SQL Server ANSI_PADDING will always be ON and any applications that explicitly set the option to OFF will produce an error. </div>
  </li>

  <li>
    <div align="left">Trailing blanks in character values inserted into varchar columns are not trimmed. </div>
  </li>
</ul>

<p align="left"><strong>SET ANSI_WARNINGS <font color="#004000">ON</font></strong></p>

<p align="left"><a href="http://msdn.microsoft.com/en-us/library/ms190368.aspx">http://msdn.microsoft.com/en-us/library/ms190368.aspx</a></p>

<ul>
  <li>
    <div align="left">When set to ON, the divide-by-zero and arithmetic overflow errors cause the statement to be rolled back and an error message is generated. When set to OFF, the divide-by-zero and arithmetic overflow errors cause null values to be returned. </div>
  </li>
</ul>

<p align="left"><strong>SET CONCAT_NULL_YIELDS_NULL <font color="#004000">ON</font></strong></p>

<p align="left"><a href="http://msdn.microsoft.com/en-us/library/ms176056.aspx">http://msdn.microsoft.com/en-us/library/ms176056.aspx</a></p>

<ul>
  <li>
    <div align="left">In a future version of SQL Server CONCAT_NULL_YIELDS_NULL will always be ON and any applications that explicitly set the option to OFF will generate an error. </div>
  </li>

  <li>
    <div align="left">When SET CONCAT_NULL_YIELDS_NULL is ON, concatenating a null value with a string yields a NULL result. For example, SELECT 'abc' + NULL yields NULL. When SET CONCAT_NULL_YIELDS_NULL is OFF, concatenating a null value with a string yields the string itself (the null value is treated as an empty string). For example, SELECT 'abc' + NULL yields abc. </div>
  </li>
</ul>

<p align="left"><strong>SET QUOTED_IDENTIFIER <font color="#004000">ON</font></strong></p>

<p align="left"><a href="http://msdn.microsoft.com/en-us/library/ms174393.aspx">http://msdn.microsoft.com/en-us/library/ms174393.aspx</a></p>

<ul>
  <li>
    <div align="left">Allows for objects to be created with reserved key words, for example a table called &quot;select&quot;. </div>
  </li>
</ul>

<p align="left"><strong>SET NUMERIC_ROUNDABORT <font color="#800000">OFF</font></strong></p>

<p align="left"><a href="http://msdn.microsoft.com/en-us/library/ms188791.aspx">http://msdn.microsoft.com/en-us/library/ms188791.aspx</a></p>

<ul>
  <li>
    <div align="left">When SET NUMERIC_ROUNDABORT is ON, an error is generated after a loss of precision occurs in an expression. When OFF, losses of precision do not generate error messages and the result is rounded to the precision of the column or variable storing the result. </div>
  </li>
</ul>

<p align="left"><strong>SET ARITHABORT <font color="#004000">ON</font></strong></p>

<p align="left"><a href="http://msdn.microsoft.com/en-us/library/ms190306.aspx">http://msdn.microsoft.com/en-us/library/ms190306.aspx</a></p>

<ul>
  <li>
    <div align="left">You should always set ARITHABORT to ON in your logon sessions. Setting ARITHABORT to OFF can negatively impact query optimization leading to performance issues. </div>
  </li>
</ul>