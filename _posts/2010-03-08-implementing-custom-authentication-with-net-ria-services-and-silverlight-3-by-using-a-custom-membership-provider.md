---
ID: 1069
post_title: >
  Implementing custom authentication with
  .NET RIA Services and Silverlight 3, by
  using a Custom Membership Provider
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/08/implementing-custom-authentication-with-net-ria-services-and-silverlight-3-by-using-a-custom-membership-provider/
published: true
post_date: 2010-03-08 09:53:26
---
<p>   <br />I am creating a Silverlight 3 application that must work with a database that is used by a legacy ASP .net 1.0 system. The database contains tables for users and roles. The Silverlight 3 application should use forms authentication and use the “User” and “Role” table in the database. </p>  <p>First I tried to change the uthenticationService : AuthenticationBase&lt;UserWeb&gt; to inherit my “LINQ to SQL” domainservice, but then I got a exception:   <br />    <br />The entity type 'Ada.Tts.Toggle.Silverlight.Web.Company' is exposed by multiple DomainService types. Entity types cannot be shared across DomainServices</p>  <p>I solved this problem by implementing a custom membership provider, the custom membership provider uses the Linq to SQL domainservice.</p>  <p><strong>TTSMembershipProvider.cs</strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Web.Security;

<span style="color: blue">namespace </span>Ada.Tts.Toggle.Web.BC
{
    <span style="color: blue">public class </span><span style="color: #2b91af">TTSMembershipProvider </span>: <span style="color: #2b91af">MembershipProvider
    </span>{
        <span style="color: blue">public override string </span>ApplicationName
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
            }
            <span style="color: blue">set
            </span>{
                <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
            }
        }
        <span style="color: blue">public override bool </span>ChangePassword(<span style="color: blue">string </span>username, <span style="color: blue">string </span>oldPassword, <span style="color: blue">string </span>newPassword)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override bool </span>ChangePasswordQuestionAndAnswer(<span style="color: blue">string </span>username, <span style="color: blue">string </span>password, <span style="color: blue">string </span>newPasswordQuestion, <span style="color: blue">string </span>newPasswordAnswer)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override </span><span style="color: #2b91af">MembershipUser </span>CreateUser(<span style="color: blue">string </span>username, <span style="color: blue">string </span>password, <span style="color: blue">string </span>email, <span style="color: blue">string </span>passwordQuestion, <span style="color: blue">string </span>passwordAnswer, <span style="color: blue">bool </span>isApproved, <span style="color: blue">object </span>providerUserKey, <span style="color: blue">out </span><span style="color: #2b91af">MembershipCreateStatus </span>status)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override bool </span>DeleteUser(<span style="color: blue">string </span>username, <span style="color: blue">bool </span>deleteAllRelatedData)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override bool </span>EnablePasswordReset
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override bool </span>EnablePasswordRetrieval
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override </span><span style="color: #2b91af">MembershipUserCollection </span>FindUsersByEmail(<span style="color: blue">string </span>emailToMatch, <span style="color: blue">int </span>pageIndex, <span style="color: blue">int </span>pageSize, <span style="color: blue">out int </span>totalRecords)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override </span><span style="color: #2b91af">MembershipUserCollection </span>FindUsersByName(<span style="color: blue">string </span>usernameToMatch, <span style="color: blue">int </span>pageIndex, <span style="color: blue">int </span>pageSize, <span style="color: blue">out int </span>totalRecords)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override </span><span style="color: #2b91af">MembershipUserCollection </span>GetAllUsers(<span style="color: blue">int </span>pageIndex, <span style="color: blue">int </span>pageSize, <span style="color: blue">out int </span>totalRecords)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override int </span>GetNumberOfUsersOnline()
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override string </span>GetPassword(<span style="color: blue">string </span>username, <span style="color: blue">string </span>answer)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override </span><span style="color: #2b91af">MembershipUser </span>GetUser(<span style="color: blue">object </span>providerUserKey, <span style="color: blue">bool </span>userIsOnline)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override </span><span style="color: #2b91af">MembershipUser </span>GetUser(<span style="color: blue">string </span>username, <span style="color: blue">bool </span>userIsOnline)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override string </span>GetUserNameByEmail(<span style="color: blue">string </span>email)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override int </span>MaxInvalidPasswordAttempts
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override int </span>MinRequiredNonAlphanumericCharacters
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override int </span>MinRequiredPasswordLength
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override int </span>PasswordAttemptWindow
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override </span><span style="color: #2b91af">MembershipPasswordFormat </span>PasswordFormat
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override string </span>PasswordStrengthRegularExpression
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override bool </span>RequiresQuestionAndAnswer
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override bool </span>RequiresUniqueEmail
        {
            <span style="color: blue">get </span>{ <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>(); }
        }
        <span style="color: blue">public override string </span>ResetPassword(<span style="color: blue">string </span>username, <span style="color: blue">string </span>answer)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override bool </span>UnlockUser(<span style="color: blue">string </span>userName)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override void </span>UpdateUser(<span style="color: #2b91af">MembershipUser </span>user)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">NotImplementedException</span>();
        }
        <span style="color: blue">public override bool </span>ValidateUser(<span style="color: blue">string </span>username, <span style="color: blue">string </span>password)
        {
            <span style="color: blue">bool </span>result = <span style="color: blue">false</span>;
            <span style="color: #2b91af">TimeTrackerDataContext </span>context = <span style="color: blue">new </span><span style="color: #2b91af">TimeTrackerDataContext</span>();
            <span style="color: blue">var </span>users = <span style="color: blue">from </span>u <span style="color: blue">in </span>context.TTUsers
                                    <span style="color: blue">where </span>u.UserName == username &amp;&amp; u.Password == <span style="color: #2b91af">Protector</span>.Encrypt(password)
                                    <span style="color: blue">select </span>u;

            <span style="color: blue">if </span>(users != <span style="color: blue">null </span>&amp;&amp; users.ToList&lt;<span style="color: #2b91af">TTUser</span>&gt;().Count &gt; 0)
            {
                    result = <span style="color: blue">true</span>;
            }
            
            <span style="color: blue">return </span>result;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br /><strong>Web.config</strong></p>
<a href="http://11011.net/software/vspaste"></a>

<pre class="code"><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot;<span style="color: blue">?&gt;
&lt;</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">sectionGroup </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">system.web.extensions</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Configuration.SystemWebExtensionsSectionGroup, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">sectionGroup </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">scripting</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Configuration.ScriptingSectionGroup, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">scriptResourceHandler</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Configuration.ScriptingScriptResourceHandlerSection, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot; <span style="color: red">requirePermission</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">allowDefinition</span><span style="color: blue">=</span>&quot;<span style="color: blue">MachineToApplication</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">sectionGroup </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">webServices</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Configuration.ScriptingWebServicesSectionGroup, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">jsonSerialization</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Configuration.ScriptingJsonSerializationSection, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot; <span style="color: red">requirePermission</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">allowDefinition</span><span style="color: blue">=</span>&quot;<span style="color: blue">Everywhere</span>&quot;<span style="color: blue">/&gt;
          &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">profileService</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Configuration.ScriptingProfileServiceSection, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot; <span style="color: red">requirePermission</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">allowDefinition</span><span style="color: blue">=</span>&quot;<span style="color: blue">MachineToApplication</span>&quot;<span style="color: blue">/&gt;
          &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">authenticationService</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Configuration.ScriptingAuthenticationServiceSection, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot; <span style="color: red">requirePermission</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">allowDefinition</span><span style="color: blue">=</span>&quot;<span style="color: blue">MachineToApplication</span>&quot;<span style="color: blue">/&gt;
          &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">roleService</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Configuration.ScriptingRoleServiceSection, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot; <span style="color: red">requirePermission</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">allowDefinition</span><span style="color: blue">=</span>&quot;<span style="color: blue">MachineToApplication</span>&quot;<span style="color: blue">/&gt;
        &lt;/</span><span style="color: #a31515">sectionGroup</span><span style="color: blue">&gt;
      &lt;/</span><span style="color: #a31515">sectionGroup</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">sectionGroup</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">appSettings</span><span style="color: blue">/&gt;
    &lt;</span><span style="color: #a31515">connectionStrings</span><span style="color: blue">&gt;
  <font size="4">&lt;</font></span><font size="4"><span style="color: #a31515">remove </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">LocalSqlServer</span>&quot; </font><font size="4"><span style="color: blue">/&gt;
  &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">LocalSqlServer</span>&quot; <span style="color: red">connectionString</span><span style="color: blue">=</span>&quot;<span style="color: blue">Data Source=.;Initial Catalog=TimeTracker;Integrated Security=True</span>&quot;
   <span style="color: red">providerName</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Data.SqlClient</span>&quot; <span style="color: blue">/&gt;</span></font><span style="color: blue">
 &lt;/</span><span style="color: #a31515">connectionStrings</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">system.web</span><span style="color: blue">&gt;
    &lt;!-- 
            </span><span style="color: green">Set compilation debug=&quot;true&quot; to insert debugging 
            symbols into the compiled page. Because this 
            affects performance, set this value to true only 
            during development.
        </span><span style="color: blue">--&gt;
    <font size="4">&lt;</font></span><font size="4"><span style="color: #a31515">roleManager </span><span style="color: red">enabled</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;</font><font size="4"><span style="color: blue">/&gt;
    &lt;</span><span style="color: #a31515">globalization </span><span style="color: red">culture</span><span style="color: blue">=</span>&quot;<span style="color: blue">auto</span>&quot;</font><font size="4"><span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">membership </span><span style="color: red">defaultProvider</span><span style="color: blue">=</span>&quot;<span style="color: blue">TTSMembershipProvider</span>&quot;</font><font size="4"><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">providers</span></font><font size="4"><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">clear</span></font><span style="color: blue"><font size="4">/&gt;
                &lt;</font></span><font size="4"><span style="color: #a31515">add
     </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">TTSMembershipProvider</span>&quot;
     <span style="color: red">type</span><span style="color: blue">=</span>&quot; <span style="color: blue">Ada.Tts.Toggle.Web.BC.TTSMembershipProvider, Ada.Tts.Toggle.Web</span>&quot;</font><font size="4"><span style="color: blue">/&gt;
            &lt;/</span><span style="color: #a31515">providers</span></font><font size="4"><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">membership</span></font><font size="4"><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">compilation </span><span style="color: red">debug</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;</font><span style="color: blue"><font size="4">&gt;</font>
      &lt;</span><span style="color: #a31515">assemblies</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">add </span><span style="color: red">assembly</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">add </span><span style="color: red">assembly</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Data.DataSetExtensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">add </span><span style="color: red">assembly</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">add </span><span style="color: red">assembly</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">assemblies</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">compilation</span><span style="color: blue">&gt;
    &lt;!--
            </span><span style="color: green">The &lt;authentication&gt; section enables configuration 
            of the security authentication mode used by 
            ASP.NET to identify an incoming user. 
        </span><span style="color: blue">--&gt;
    <font size="4">&lt;</font></span><font size="4"><span style="color: #a31515">authentication </span><span style="color: red">mode</span><span style="color: blue">=</span>&quot;<span style="color: blue">Forms</span>&quot;</font><font size="4"><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">forms </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">.Ada.Tts.Toggle_ASPXAUTH</span>&quot; </font><font size="4"><span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">authentication</span></font><span style="color: blue"><font size="4">&gt;</font>
    &lt;!--
            </span><span style="color: green">The &lt;customErrors&gt; section enables configuration 
            of what to do if/when an unhandled error occurs 
            during the execution of a request. Specifically, 
            it enables developers to configure html error pages 
            to be displayed in place of a error stack trace.

        &lt;customErrors mode=&quot;RemoteOnly&quot; defaultRedirect=&quot;GenericErrorPage.htm&quot;&gt;
            &lt;error statusCode=&quot;403&quot; redirect=&quot;NoAccess.htm&quot; /&gt;
            &lt;error statusCode=&quot;404&quot; redirect=&quot;FileNotFound.htm&quot; /&gt;
        &lt;/customErrors&gt;
        </span><span style="color: blue">--&gt;
    &lt;</span><span style="color: #a31515">profile</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">properties</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">FriendlyName</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">properties</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">profile</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">pages</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">controls</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">add </span><span style="color: red">tagPrefix</span><span style="color: blue">=</span>&quot;<span style="color: blue">asp</span>&quot; <span style="color: red">namespace</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.UI</span>&quot; <span style="color: red">assembly</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">add </span><span style="color: red">tagPrefix</span><span style="color: blue">=</span>&quot;<span style="color: blue">asp</span>&quot; <span style="color: red">namespace</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.UI.WebControls</span>&quot; <span style="color: red">assembly</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">controls</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">pages</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">httpHandlers</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">path</span><span style="color: blue">=</span>&quot;<span style="color: blue">*.asmx</span>&quot; <span style="color: red">verb</span><span style="color: blue">=</span>&quot;<span style="color: blue">*</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Script.Services.ScriptHandlerFactory, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot; <span style="color: red">validate</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">path</span><span style="color: blue">=</span>&quot;<span style="color: blue">*_AppService.axd</span>&quot; <span style="color: red">verb</span><span style="color: blue">=</span>&quot;<span style="color: blue">*</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Script.Services.ScriptHandlerFactory, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot; <span style="color: red">validate</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">path</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptResource.axd</span>&quot; <span style="color: red">verb</span><span style="color: blue">=</span>&quot;<span style="color: blue">GET,HEAD</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Handlers.ScriptResourceHandler, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot; <span style="color: red">validate</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">httpHandlers</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">httpModules</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptModule</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Handlers.ScriptModule, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">DomainServiceModule</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Ria.Services.DomainServiceHttpModule, System.Web.Ria, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">httpModules</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">system.web</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">system.codedom</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">compilers</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">compiler </span><span style="color: red">language</span><span style="color: blue">=</span>&quot;<span style="color: blue">c#;cs;csharp</span>&quot; <span style="color: red">extension</span><span style="color: blue">=</span>&quot;<span style="color: blue">.cs</span>&quot; <span style="color: red">warningLevel</span><span style="color: blue">=</span>&quot;<span style="color: blue">4</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">Microsoft.CSharp.CSharpCodeProvider, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">providerOption </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">CompilerVersion</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">v3.5</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">providerOption </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">WarnAsError</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">compiler</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">compilers</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">system.codedom</span><span style="color: blue">&gt;
  &lt;!-- 
        </span><span style="color: green">The system.webServer section is required for running ASP.NET AJAX under Internet
        Information Services 7.0.  It is not necessary for previous version of IIS.
  </span><span style="color: blue">--&gt;
  &lt;</span><span style="color: #a31515">system.webServer</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">validation </span><span style="color: red">validateIntegratedModeConfiguration</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot;<span style="color: blue">/&gt;
    &lt;</span><span style="color: #a31515">modules</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">remove </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptModule</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptModule</span>&quot; <span style="color: red">preCondition</span><span style="color: blue">=</span>&quot;<span style="color: blue">managedHandler</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Handlers.ScriptModule, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">DomainServiceModule</span>&quot; <span style="color: red">preCondition</span><span style="color: blue">=</span>&quot;<span style="color: blue">managedHandler</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Ria.Services.DomainServiceHttpModule, System.Web.Ria, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">modules</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">handlers</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">remove </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">WebServiceHandlerFactory-Integrated</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">remove </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptHandlerFactory</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">remove </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptHandlerFactoryAppServices</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">remove </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptResource</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptHandlerFactory</span>&quot; <span style="color: red">verb</span><span style="color: blue">=</span>&quot;<span style="color: blue">*</span>&quot; <span style="color: red">path</span><span style="color: blue">=</span>&quot;<span style="color: blue">*.asmx</span>&quot; <span style="color: red">preCondition</span><span style="color: blue">=</span>&quot;<span style="color: blue">integratedMode</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Script.Services.ScriptHandlerFactory, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptHandlerFactoryAppServices</span>&quot; <span style="color: red">verb</span><span style="color: blue">=</span>&quot;<span style="color: blue">*</span>&quot; <span style="color: red">path</span><span style="color: blue">=</span>&quot;<span style="color: blue">*_AppService.axd</span>&quot; <span style="color: red">preCondition</span><span style="color: blue">=</span>&quot;<span style="color: blue">integratedMode</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Script.Services.ScriptHandlerFactory, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptResource</span>&quot; <span style="color: red">preCondition</span><span style="color: blue">=</span>&quot;<span style="color: blue">integratedMode</span>&quot; <span style="color: red">verb</span><span style="color: blue">=</span>&quot;<span style="color: blue">GET,HEAD</span>&quot; <span style="color: red">path</span><span style="color: blue">=</span>&quot;<span style="color: blue">ScriptResource.axd</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Handlers.ScriptResourceHandler, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">handlers</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">system.webServer</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">runtime</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">assemblyBinding </span><span style="color: red">xmlns</span><span style="color: blue">=</span>&quot;<span style="color: blue">urn:schemas-microsoft-com:asm.v1</span>&quot;<span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">dependentAssembly</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">assemblyIdentity </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Extensions</span>&quot; <span style="color: red">publicKeyToken</span><span style="color: blue">=</span>&quot;<span style="color: blue">31bf3856ad364e35</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">bindingRedirect </span><span style="color: red">oldVersion</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0.0.0-1.1.0.0</span>&quot; <span style="color: red">newVersion</span><span style="color: blue">=</span>&quot;<span style="color: blue">3.5.0.0</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">dependentAssembly</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">dependentAssembly</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">assemblyIdentity </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Extensions.Design</span>&quot; <span style="color: red">publicKeyToken</span><span style="color: blue">=</span>&quot;<span style="color: blue">31bf3856ad364e35</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">bindingRedirect </span><span style="color: red">oldVersion</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0.0.0-1.1.0.0</span>&quot; <span style="color: red">newVersion</span><span style="color: blue">=</span>&quot;<span style="color: blue">3.5.0.0</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">dependentAssembly</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">assemblyBinding</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">runtime</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">system.serviceModel</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">serviceHostingEnvironment </span><span style="color: red">aspNetCompatibilityEnabled</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;<span style="color: blue">/&gt;
  &lt;/</span><span style="color: #a31515">system.serviceModel</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>For more information on implementing a custom roleprovider, see:</p>

<p><a title="http://davidhayden.com/blog/dave/archive/2007/10/17/CreateCustomRoleProviderASPNETRolePermissionsSecurity.aspx" href="http://davidhayden.com/blog/dave/archive/2007/10/17/CreateCustomRoleProviderASPNETRolePermissionsSecurity.aspx">http://davidhayden.com/blog/dave/archive/2007/10/17/CreateCustomRoleProviderASPNETRolePermissionsSecurity.aspx</a></p>