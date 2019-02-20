---
ID: 2703
post_title: >
  Simplest way to add forms authentication
  to you Web.config in ASP .NET, when
  using AspNetSqlMembershipProvider
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/05/24/simplest-way-to-add-forms-authentication-to-you-web-config-in-asp-net-when-using-aspnetsqlmembershipprovider/
published: true
post_date: 2012-05-24 16:44:38
---
<p>If you’ve got a website and this website contains a Login.aspx and a Default.aspx page in the root.</p>  <p>The simplest way to deny all unauthenticated user access to the website is adding the following to you’re Web.config:</p>  <pre class="code"> <span style="color: blue">&lt;</span><span style="color: #a31515">system.web</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">authentication </span><span style="color: red">mode</span><span style="color: blue">=</span>&quot;<span style="color: blue">Forms</span>&quot;<span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">forms </span><span style="color: red">loginUrl</span><span style="color: blue">=</span>&quot;<span style="color: blue">Login.aspx</span>&quot;
           <span style="color: red">protection</span><span style="color: blue">=</span>&quot;<span style="color: blue">All</span>&quot;
           <span style="color: red">timeout</span><span style="color: blue">=</span>&quot;<span style="color: blue">30</span>&quot;
           <span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">.ASPXAUTH</span>&quot;
           <span style="color: red">path</span><span style="color: blue">=</span>&quot;<span style="color: blue">/</span>&quot;
           <span style="color: red">requireSSL</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot;
           <span style="color: red">slidingExpiration</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;
           <span style="color: red">defaultUrl</span><span style="color: blue">=</span>&quot;<span style="color: blue">Default.aspx</span>&quot;
           <span style="color: red">cookieless</span><span style="color: blue">=</span>&quot;<span style="color: blue">UseDeviceProfile</span>&quot;
           <span style="color: red">enableCrossAppRedirects</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">authentication</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">authorization</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">deny </span><span style="color: red">users</span><span style="color: blue">=</span>&quot;<span style="color: blue">?</span>&quot; <span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">authorization</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">membership</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">providers</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">clear </span><span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">add </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">AspNetSqlMembershipProvider</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Web.Security.SqlMembershipProvider</span>&quot; <span style="color: red">connectionStringName</span><span style="color: blue">=</span>&quot;<span style="color: blue">ApplicationServices</span>&quot; <span style="color: red">enablePasswordRetrieval</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">enablePasswordReset</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot; <span style="color: red">requiresQuestionAndAnswer</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">requiresUniqueEmail</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">maxInvalidPasswordAttempts</span><span style="color: blue">=</span>&quot;<span style="color: blue">5</span>&quot; <span style="color: red">minRequiredPasswordLength</span><span style="color: blue">=</span>&quot;<span style="color: blue">6</span>&quot; <span style="color: red">minRequiredNonalphanumericCharacters</span><span style="color: blue">=</span>&quot;<span style="color: blue">0</span>&quot; <span style="color: red">passwordAttemptWindow</span><span style="color: blue">=</span>&quot;<span style="color: blue">10</span>&quot; <span style="color: red">applicationName</span><span style="color: blue">=</span>&quot;<span style="color: blue">/</span>&quot; <span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">providers</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">membership</span><span style="color: blue">&gt;
 </span><span style="color: blue">&lt;/</span><span style="color: #a31515">system.web</span><span style="color: blue">&gt;
</span></pre>


<p>&#160;</p>

<p>This ensures that unauthenticated user can only access the Login.aspx and no other resources, accept the resources needed by the Login.aspx. So if the Login.aspx uses a /Images/Logo.png this images will show on the Login.aspx. Accessing the image directly by an unauthenticated user will redirect this user back to the Login.aspx page.</p>