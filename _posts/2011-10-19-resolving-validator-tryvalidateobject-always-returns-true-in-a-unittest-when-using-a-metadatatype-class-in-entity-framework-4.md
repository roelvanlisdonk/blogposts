---
ID: 2174
post_title: 'Resolving: Validator.TryValidateObject always returns true in a UnitTest, when using a MetadataType class in Entity Framework 4'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/10/19/resolving-validator-tryvalidateobject-always-returns-true-in-a-unittest-when-using-a-metadatatype-class-in-entity-framework-4/
published: true
post_date: 2011-10-19 14:16:35
---
<p align="left">When you use a metadata class in Entity Framework the registration between the entity and the metadata class is not registered for all Microsoft Visual Studio Project types (the &quot;test project class library&quot; for example).</p>  <p align="left">I found the solution at: <a title="http://stackoverflow.com/questions/2657358/net-4-rtm-metadatatype-attribute-ignored-when-using-validator" href="http://stackoverflow.com/questions/2657358/net-4-rtm-metadatatype-attribute-ignored-when-using-validator">http://stackoverflow.com/questions/2657358/net-4-rtm-metadatatype-attribute-ignored-when-using-validator</a>. It demonstrates registring all metadata classes in an assembly.</p>  <p align="left">&#160;</p>  <p align="left"><strong>Solution</strong></p>  <p align="left">Add the following class, to the assembly that contains the Entity Framework model (*.edmx) and the metadata classes:</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.ComponentModel;
<span style="color: blue">using </span>System.ComponentModel.DataAnnotations;
<span style="color: blue">using </span>System.Reflection;

<span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Metadata classes are not always automatically registered, for example in a UnitTest classlibrary.
</span><span style="color: gray">/// </span><span style="color: green">This class can be used to register all metadata classes find in this assembly.
</span><span style="color: gray">/// 
/// </span><span style="color: green">Registration will only be done once.
</span><span style="color: gray">/// &lt;/summary&gt;
</span><span style="color: blue">public static class </span><span style="color: #2b91af">MetadataTypesRegister
</span>{
    <span style="color: blue">private static bool </span>_installed = <span style="color: blue">false</span>;
    <span style="color: blue">private static readonly object </span>InstalledLock = <span style="color: blue">new object</span>();


    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Register all metadata classes found in this assembly.
    </span><span style="color: gray">/// </span><span style="color: green">Registration will only be done once.        
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span><span style="color: blue">public static void </span>InstallForAssembly()
    {
        <span style="color: blue">if </span>(_installed)
        {
            <span style="color: blue">return</span>;
        }

        <span style="color: blue">lock </span>(InstalledLock)
        {
            <span style="color: blue">if </span>(_installed)
            {
                <span style="color: blue">return</span>;
            }

            <span style="color: blue">foreach </span>(<span style="color: #2b91af">Type </span>type <span style="color: blue">in </span><span style="color: #2b91af">Assembly</span>.GetExecutingAssembly().GetTypes())
            {
                <span style="color: blue">foreach </span>(<span style="color: #2b91af">MetadataTypeAttribute </span>attrib <span style="color: blue">in </span>type.GetCustomAttributes(<span style="color: blue">typeof</span>(<span style="color: #2b91af">MetadataTypeAttribute</span>), <span style="color: blue">true</span>))
                {
                    <span style="color: #2b91af">TypeDescriptor</span>.AddProviderTransparent(<span style="color: blue">new </span><span style="color: #2b91af">AssociatedMetadataTypeTypeDescriptionProvider</span>(type, attrib.MetadataClassType), type);
                }
            }

            _installed = <span style="color: blue">true</span>;
        }
    }
}</pre>

<p align="left">&#160;</p>

<p align="left">In entity framework, you define metadata attributes in an internal sealed metadata &quot;buddy&quot; class like:</p>

<pre class="code">[<span style="color: #2b91af">MetadataType</span>(<span style="color: blue">typeof</span>(<span style="color: #2b91af">CustomerMetadata</span>))]
    <span style="color: blue">public partial class </span><span style="color: #2b91af">Customer
    </span>{
        <span style="color: blue">internal sealed class </span><span style="color: #2b91af">CustomerMetadata
        </span>{

            [<span style="color: #2b91af">Required</span>(ErrorMessage = <span style="color: #a31515">&quot;Id is required&quot;</span>)]
            <span style="color: blue">public </span><span style="color: #2b91af">Int32 </span>Id { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

            [<span style="color: #2b91af">Required</span>(ErrorMessage = <span style="color: #a31515">&quot;Name is required&quot;</span>)]
            <span style="color: blue">public </span><span style="color: #2b91af">String </span>Name { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

            [<span style="color: #2b91af">DataType</span>(<span style="color: #2b91af">DataType</span>.EmailAddress)]
            <span style="color: blue">public </span><span style="color: #2b91af">String </span>Email { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

            [<span style="color: #2b91af">RegularExpression</span>(<span style="color: #a31515">&quot;^[0-9]{4}[a-z|A-Z]{2}$&quot;</span>)]
            <span style="color: blue">public </span><span style="color: #2b91af">String </span>Zipcode { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

        }
    }</pre>

<p>You can unit test the metadata attributes by using the following unit test class.</p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;
<span style="color: blue">using </span>Research.Dal2;
<span style="color: blue">using </span>System.ComponentModel.DataAnnotations;

[<span style="color: #2b91af">TestClass</span>]
<span style="color: blue">public class </span><span style="color: #2b91af">CustomerTester
</span>{
    <span style="color: blue">private </span><span style="color: #2b91af">TestContext </span>testContextInstance;

    <span style="color: gray">/// &lt;summary&gt;
    ///</span><span style="color: green">Gets or sets the test context which provides
    </span><span style="color: gray">///</span><span style="color: green">information about and functionality for the current test run.
    </span><span style="color: gray">///&lt;/summary&gt;
    </span><span style="color: blue">public </span><span style="color: #2b91af">TestContext </span>TestContext
    {
        <span style="color: blue">get
        </span>{
            <span style="color: blue">return </span>testContextInstance;
        }
        <span style="color: blue">set
        </span>{
            testContextInstance = <span style="color: blue">value</span>;
        }
    }

    [<span style="color: #2b91af">ClassInitialize</span>()]
    <span style="color: blue">public static void </span>MyClassInitialize(<span style="color: #2b91af">TestContext </span>testContext) 
    {
        <span style="color: #2b91af">MetadataTypesRegister</span>.InstallForAssembly();
    }
    
    [<span style="color: #2b91af">TestMethod</span>]
    <span style="color: blue">public void </span>ValidateZipcodeTest()
    {
        <span style="color: blue">var </span>customer = <span style="color: blue">new </span>Research.Dal2.<span style="color: #2b91af">Customer</span>();
        customer.Zipcode = <span style="color: #a31515">&quot;this is a wrong zipcode&quot;</span>;
        <span style="color: blue">var </span>vc = <span style="color: blue">new </span><span style="color: #2b91af">ValidationContext</span>(customer, <span style="color: blue">null</span>, <span style="color: blue">null</span>) { MemberName = <span style="color: #a31515">&quot;Zipcode&quot; </span>};
        <span style="color: blue">var </span>validationResults = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">ValidationResult</span>&gt;();

        <span style="color: green">// Validate only the zip code.
        </span><span style="color: blue">bool </span>isValidZipCode = <span style="color: #2b91af">Validator</span>.TryValidateProperty(customer.Zipcode, vc, validationResults);
        <span style="color: #2b91af">Assert</span>.IsFalse(isValidZipCode);

        <span style="color: green">// Validate the whole Customer entity.
        </span><span style="color: blue">bool </span>isValidCustomer = <span style="color: #2b91af">Validator</span>.TryValidateObject(customer, vc, validationResults, <span style="color: blue">true</span>);
        <span style="color: #2b91af">Assert</span>.IsFalse(isValidCustomer);
    }
}</pre>


<p style="padding-bottom: 0px; line-height: 13pt; margin: 0cm 0cm 10pt; text-autospace: ; mso-pagination: none; mso-layout-grid-align: none" class="MsoNormal" align="left"><span style="mso-ansi-language: en; mso-ascii-font-family: calibri; mso-hansi-font-family: calibri; mso-bidi-font-family: calibri" lang="EN"><font face="Calibri"><font style="font-size: 11pt" color="#000000">&#160;</font></font></span></p>