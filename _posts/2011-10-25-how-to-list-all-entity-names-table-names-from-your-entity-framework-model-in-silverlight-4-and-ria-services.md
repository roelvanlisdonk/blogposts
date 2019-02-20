---
ID: 2183
post_title: >
  How to list all entity names / table
  names from your Entity Framework model
  in Silverlight 4 and RIA services
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/10/25/how-to-list-all-entity-names-table-names-from-your-entity-framework-model-in-silverlight-4-and-ria-services/
published: true
post_date: 2011-10-25 11:20:11
---
<p>If you want to list all entity names / table names from your Entity Framework model (*.edmx) in Silverlight 4, use a RIA Invoke operation:</p>  <p>&#160;</p>  <p>   <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Data.Metadata.Edm;
<span style="color: blue">using </span>System.ServiceModel.DomainServices.Server;

<span style="color: blue">namespace </span>Research.Web
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">ResearchDomainService
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Get the entity names from the entity framework model on which this DomainService is generated.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;returns&gt;
        /// </span><span style="color: green">A list of entity / table names
        </span><span style="color: gray">/// &lt;/returns&gt;
        </span>[<span style="color: #2b91af">Invoke</span>]
        <span style="color: blue">public </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; GetEntityTypeNames()
        {
            <span style="color: #2b91af">EntityContainer </span>container = ObjectContext.MetadataWorkspace.GetEntityContainer(ObjectContext.DefaultContainerName, <span style="color: #2b91af">DataSpace</span>.CSpace);
            <span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; result = (<span style="color: blue">from </span>meta <span style="color: blue">in </span>container.BaseEntitySets
                      <span style="color: blue">where </span>meta.BuiltInTypeKind == <span style="color: #2b91af">BuiltInTypeKind</span>.EntitySet
                      <span style="color: blue">select </span>meta.ElementType.ToString()).ToList&lt;<span style="color: blue">string</span>&gt;();

            <span style="color: blue">return </span>result;
        }
    }
}</pre>
</p>

<p>If the database contains the following tables:</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image4.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image_thumb4.png" width="244" height="231" /></a></p>

<p>&#160;</p>

<p>The list will contain the strings:</p>

<p>ResearchModel.Customer</p>

<p>ResearchModel.Person</p>

<p>ResearchModel.Product</p>

<p>ResearchModel.ProductTag</p>

<p>ResearchModel.Tag</p>