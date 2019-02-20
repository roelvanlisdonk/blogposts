---
ID: 3197
post_title: 'ASP .NET MVC4 / Web Api &#8211; Create users and roles for SimpleMembershipProvider with PowerShell and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/15/asp-net-mvc4-web-api-create-users-and-roles-for-simplemembershipprovider-with-powershell-and-c/
published: true
post_date: 2013-04-15 11:59:32
---
<p>If you are using the SimpleMembershipProvider for FormAuthentication in a ASP .NET MVC4 / Web Api project, the following PowerShell / C# code can be used to create and delete users and roles.</p>  <ul>   <li>Create an empty XML App.config file &quot;C:\Temp\App.config&quot;. </li>    <li>Paste the XML below in the file and save it. </li>    <li>Create an empty PowerShell file &quot;C:\Temp\Manage_MVC_users_and_roles.ps1&quot;. </li>    <li>Paste the PowerShell code below in the file and save it.      <ul><!--EndFragment--></ul>   </li>    <li>Create an empty C# file &quot;C:\Temp\Manage_MVC_users_and_roles.cs&quot;. </li>    <li>Paste the C# code below in the file and save it. </li>    <li>Execute the file &quot;C:\Temp\Manage_MVC_users_and_roles.ps1&quot; with PowerShell. </li> </ul>  <p>&#160;</p>  <p>This will create an user &quot;test2&quot; with password &quot;test2&quot; and a role &quot;Administrators&quot;.</p>  <p>&#160;</p>  <p><strong>Note</strong></p>  <ul>   <li>Database tables will automatically be created if they don’t exist. </li>    <li>De folder &quot;C:\Temp&quot; should contain the assemblies &quot;System.Web.WebPages.dll&quot; and &quot;WebMatrix.Data.dll&quot; and &quot;WebMatrix.WebData.dll&quot;, this assembly can be downloaded using NuGet. </li> </ul>  <p><strong>App.config</strong></p>  <pre class="code"><span style="background: white; color: blue">&lt;?</span><span style="background: white; color: #a31515">xml </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">1.0</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">encoding</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">utf-8</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">?&gt;
&lt;</span><span style="background: white; color: #a31515">configuration</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">system.web</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">profile </span><span style="background: white; color: red">defaultProvider</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">SimpleProfileProvider</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">&gt;
      &lt;</span><span style="background: white; color: #a31515">providers</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: #a31515">add </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">SimpleProfileProvider</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">WebMatrix.WebData.SimpleMembershipProvider, WebMatrix.WebData</span><span style="background: white; color: black">&quot;
            </span><span style="background: white; color: red">connectionStringName</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">DefaultConnection</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">applicationName</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">/</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
      &lt;/</span><span style="background: white; color: #a31515">providers</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: #a31515">profile</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">membership </span><span style="background: white; color: red">defaultProvider</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">SimpleMembershipProvider</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">&gt;
      &lt;</span><span style="background: white; color: #a31515">providers</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: #a31515">add </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">SimpleMembershipProvider</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">WebMatrix.WebData.SimpleMembershipProvider, WebMatrix.WebData</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
      &lt;/</span><span style="background: white; color: #a31515">providers</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: #a31515">membership</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">roleManager </span><span style="background: white; color: red">enabled</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">true</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">defaultProvider</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">SimpleRoleProvider</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">&gt;
      &lt;</span><span style="background: white; color: #a31515">providers</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: #a31515">add </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">SimpleRoleProvider</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">WebMatrix.WebData.SimpleRoleProvider, WebMatrix.WebData</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">/&gt;
      &lt;/</span><span style="background: white; color: #a31515">providers</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: #a31515">roleManager</span><span style="background: white; color: blue">&gt;
  &lt;/</span><span style="background: white; color: #a31515">system.web</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">runtime</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">assemblyBinding </span><span style="background: white; color: red">xmlns</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">urn:schemas-microsoft-com:asm.v1</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: #a31515">assemblyBinding</span><span style="background: white; color: blue">&gt;
  &lt;/</span><span style="background: white; color: #a31515">runtime</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: #a31515">configuration</span><span style="background: white; color: blue">&gt;</span></pre>

<p><strong>PowerShell code (Manage_MVC_users_and_roles.ps1)</strong></p>



<pre class="code"> 
<span style="color: #006400"># Get folder containing this script.
</span><span style="color: #ff4500">$scriptFolder </span><span style="color: #a9a9a9">= </span><span style="color: blue">split-path </span><span style="color: #ff4500">$SCRIPT:MyInvocation</span><span style="color: #a9a9a9">.</span>MyCommand<span style="color: #a9a9a9">.</span>Path <span style="color: navy">-parent

</span><span style="color: #006400"># Load App.config file from scriptfolder.
</span><span style="color: #ff4500">$appConfigPath </span><span style="color: #a9a9a9">= </span><span style="color: darkred">&quot;</span><span style="color: #ff4500">$scriptFolder</span><span style="color: darkred">\App.config&quot;
</span><span style="color: #a9a9a9">[</span><span style="color: teal">System.AppDomain</span><span style="color: #a9a9a9">]::</span>CurrentDomain<span style="color: #a9a9a9">.</span>SetData(<span style="color: darkred">&quot;APP_CONFIG_FILE&quot;</span><span style="color: #a9a9a9">, </span><span style="color: #ff4500">$appConfigPath</span>)

<span style="color: #006400"># Compile C# code to dll.
</span><span style="color: #ff4500">$Assem </span><span style="color: #a9a9a9">= </span>( 
    <span style="color: darkred">&quot;WebMatrix.Data&quot;</span><span style="color: #a9a9a9">, 
    </span><span style="color: darkred">&quot;WebMatrix.WebData&quot;</span><span style="color: #a9a9a9">,
    </span><span style="color: darkred">&quot;System.Security&quot;</span><span style="color: #a9a9a9">,
    </span><span style="color: darkred">&quot;System.Web&quot;</span><span style="color: #a9a9a9">,
    </span><span style="color: darkred">&quot;System.Web.WebPages&quot;</span><span style="color: #a9a9a9">,
    </span><span style="color: darkred">'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'</span><span style="color: #a9a9a9">,
    </span><span style="color: darkred">'System.Configuration, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'
</span>)
<span style="color: #ff4500">$codePath </span><span style="color: #a9a9a9">= </span><span style="color: darkred">&quot;</span><span style="color: #ff4500">$scriptFolder</span><span style="color: darkred">\Manage_MVC_users_and_roles.cs&quot;
</span><span style="color: #ff4500">$codeAssemblyName </span><span style="color: #a9a9a9">= </span><span style="color: darkred">&quot;Manage_MVC_users_and_roles.dll&quot;
</span><span style="color: blue">Add-Type </span><span style="color: navy">-OutputType </span><span style="color: #8a2be2">Library </span><span style="color: navy">–ReferencedAssemblies </span><span style="color: #ff4500">$Assem </span><span style="color: navy">-OutputAssembly </span><span style="color: #ff4500">$codeAssemblyName </span><span style="color: navy">-Path </span><span style="color: #ff4500">$codePath

</span><span style="color: #006400"># Load dll.
</span><span style="color: #ff4500">$codeAssemblyPath </span><span style="color: #a9a9a9">= </span><span style="color: darkred">&quot;</span><span style="color: #ff4500">$scriptFolder</span><span style="color: darkred">\</span><span style="color: #ff4500">$codeAssemblyName</span><span style="color: darkred">&quot;
</span><span style="color: blue">Add-Type </span><span style="color: navy">-Path </span><span style="color: #ff4500">$codeAssemblyPath

</span><span style="color: #006400"># Execute C# code.
</span><span style="color: #ff4500">$wrapper </span><span style="color: #a9a9a9">= </span><span style="color: blue">New-Object </span><span style="color: #8a2be2">Research.Rli.WebSecurityExecuter
</span><span style="color: #ff4500">$wrapper</span><span style="color: #a9a9a9">.</span>Execute(<span style="color: #ff4500">$scriptFolder</span>);

<span style="color: blue">pause
 
</span></pre>
<strong>C# code</strong>



<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Rli
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
    </span><span style="background: white; color: blue">public interface </span><span style="background: white; color: #2b91af">IWebSecurityExecuter
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">Execute(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">scriptFolder);
    }

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">WebSecurityExecuter </span><span style="background: white; color: black">: IWebSecurityExecuter
    {
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Executes code found in the [WebSecurityWrapper] class in a new .net AppDomain, 
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">To prevent assembly load errors, a new AppDomain is created, with the ApplicationBase set to the folder containing this *.cs file.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;scriptFolder&quot;&gt;
        /// </span><span style="background: white; color: green">Folder containing this *.cs file.
        </span><span style="background: white; color: gray">/// &lt;/param&gt;
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Execute(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">scriptFolder)
        {
            System.</span><span style="background: white; color: #2b91af">AppDomain </span><span style="background: white; color: black">childDomain = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">try
            </span><span style="background: white; color: black">{
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">domainSetup = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.</span><span style="background: white; color: #2b91af">AppDomainSetup</span><span style="background: white; color: black">()
                {
                    ApplicationBase = scriptFolder,
                    ConfigurationFile = System.</span><span style="background: white; color: #2b91af">AppDomain</span><span style="background: white; color: black">.CurrentDomain.SetupInformation.ConfigurationFile,
                    ApplicationName = System.</span><span style="background: white; color: #2b91af">AppDomain</span><span style="background: white; color: black">.CurrentDomain.SetupInformation.ApplicationName,
                    LoaderOptimization = System.</span><span style="background: white; color: #2b91af">LoaderOptimization</span><span style="background: white; color: black">.MultiDomainHost
                };
                childDomain = System.</span><span style="background: white; color: #2b91af">AppDomain</span><span style="background: white; color: black">.CreateDomain(</span><span style="background: white; color: #a31515">&quot;NewAppDomain&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">, domainSetup);
                IWebSecurityWrapper wrapper = (IWebSecurityWrapper)childDomain.CreateInstanceAndUnwrap(</span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(WebSecurityWrapper).Assembly.FullName, </span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(WebSecurityWrapper).FullName);
                wrapper.Initialize();
                wrapper.CreateUsers();
                wrapper.CreateRoles();
            }
            </span><span style="background: white; color: blue">finally
            </span><span style="background: white; color: black">{
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(childDomain != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">) System.</span><span style="background: white; color: #2b91af">AppDomain</span><span style="background: white; color: black">.Unload(childDomain);
            }
        }
    }
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">WebSecurityWrapper </span><span style="background: white; color: black">: System.</span><span style="background: white; color: #2b91af">MarshalByRefObject</span><span style="background: white; color: black">, IWebSecurityWrapper
    {
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Initializes the database connection and creates tabels, when these tables do not exist.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Initialize()
        {
            DatabaseConnectionString = </span><span style="background: white; color: #a31515">@&quot;Data Source=(LocalDb)\v11.0;Initial Catalog=MyDatabase;Integrated Security=SSPI;&quot;</span><span style="background: white; color: black">;
            Roles = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Collections.Generic.</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;
                    {
                        </span><span style="background: white; color: #a31515">&quot;Administrators&quot;
                    </span><span style="background: white; color: black">};
            Users = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Collections.Generic.</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;User&gt; 
                    { 
                        </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">User { Name = </span><span style="background: white; color: #a31515">&quot;test2&quot;</span><span style="background: white; color: black">, Password = </span><span style="background: white; color: #a31515">&quot;test2&quot;</span><span style="background: white; color: black">}
                    };
            UserIdColumnName = </span><span style="background: white; color: #a31515">&quot;UserId&quot;</span><span style="background: white; color: black">;
            UserNameColumnName = </span><span style="background: white; color: #a31515">&quot;UserName&quot;</span><span style="background: white; color: black">;
            UserTableName = </span><span style="background: white; color: #a31515">&quot;UserProfile&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: green">// Creates user and role tables if they don't exist.
            </span><span style="background: white; color: black">WebMatrix.WebData.WebSecurity.InitializeDatabaseConnection(DatabaseConnectionString, </span><span style="background: white; color: #a31515">&quot;System.Data.SqlClient&quot;</span><span style="background: white; color: black">, UserTableName, UserIdColumnName, UserNameColumnName, </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">);
        }

        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">DatabaseConnectionString { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">System.Collections.Generic.</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; Roles { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">System.Collections.Generic.</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;User&gt; Users { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">UserIdColumnName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">UserNameColumnName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">UserTableName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">CreateRoles()
        {
            Roles.ForEach(x =&gt;
            {
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">roles = (WebMatrix.WebData.SimpleRoleProvider)System.Web.Security.Roles.Provider;
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(roles.RoleExists(x))
                {
                    System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;Role [{0}] already exists.&quot;</span><span style="background: white; color: black">, x);
                }
                </span><span style="background: white; color: blue">else
                </span><span style="background: white; color: black">{
                    roles.CreateRole(x);
                }
            });
        }
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">CreateUsers()
        {
            Users.ForEach(x =&gt;
            {
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(WebMatrix.WebData.WebSecurity.UserExists(x.Name))
                {
                    System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;User [{0}] already exists.&quot;</span><span style="background: white; color: black">, x.Name);
                }
                </span><span style="background: white; color: blue">else
                </span><span style="background: white; color: black">{
                    WebMatrix.WebData.WebSecurity.CreateUserAndAccount(x.Name, x.Password);
                }
                
            });
        }
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">DeleteRoles()
        {
            Roles.ForEach(x =&gt;
            {
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">roles = (WebMatrix.WebData.SimpleRoleProvider)System.Web.Security.Roles.Provider;
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(roles.RoleExists(x))
                {
                    System.Collections.Generic.</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; usersInRole = roles.GetUsersInRole(x).ToList();
                    Users = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Collections.Generic.</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;User&gt;();
                    usersInRole.ForEach(u =&gt;
                    {
                        Users.Add(</span><span style="background: white; color: blue">new </span><span style="background: white; color: black">User { Name = u });
                    });
                    DeleteUsers();
                    roles.DeleteRole(x, </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">);
                }
                </span><span style="background: white; color: blue">else
                </span><span style="background: white; color: black">{
                    System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;Role [{0}] already exists.&quot;</span><span style="background: white; color: black">, x);
                }
            });
        }
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">DeleteUsers()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">membership = (WebMatrix.WebData.SimpleMembershipProvider)System.Web.Security.Membership.Provider;
            Users.ForEach(x =&gt;
            {
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(WebMatrix.WebData.WebSecurity.UserExists(x.Name))
                {
                    membership.DeleteAccount(x.Name);
                    membership.DeleteUser(x.Name, </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">);
                }
                </span><span style="background: white; color: blue">else
                </span><span style="background: white; color: black">{
                    System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;User [{0}] does not exist.&quot;</span><span style="background: white; color: black">, x.Name);
                }
            });
        }
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ResetPasswordUsers()
        {
            Users.ForEach(x =&gt;
            {
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(WebMatrix.WebData.WebSecurity.UserExists(x.Name))
                {
                    WebMatrix.WebData.WebSecurity.ResetPassword(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">, x.Name);
                }
                </span><span style="background: white; color: blue">else
                </span><span style="background: white; color: black">{
                    System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;User [{0}] does not exist.&quot;</span><span style="background: white; color: black">, x.Name);
                }
            });
        }
    }
    </span><span style="background: white; color: blue">public interface </span><span style="background: white; color: #2b91af">IWebSecurityWrapper
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">CreateRoles();
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">CreateUsers();
        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">DatabaseConnectionString { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">DeleteRoles();
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">DeleteUsers();
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">Initialize();
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">ResetPasswordUsers();
        System.Collections.Generic.</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; Roles { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">UserIdColumnName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">UserNameColumnName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        System.Collections.Generic.</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;Research.Rli.User&gt; Users { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">UserTableName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">User
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Name { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Password { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }
}</span></pre>