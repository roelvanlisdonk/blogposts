---
ID: 2179
post_title: 'Solving: DisplayName not showing in a DataForm in Silverlight 4 by using data annotations on a metadata class.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/10/24/solving-displayname-not-showing-in-a-dataform-in-silverlight-4-by-using-data-annotations-on-a-metadata-class/
published: true
post_date: 2011-10-24 15:40:54
---
<p>I was trying to change the displayname of a field in a dataform by placing the DisplayName attribute on the property in the metadata class. This will not work instead you must use the [Display(Name= &quot;This is the correct display name&quot;)] attribute on the field in a metadata class:</p>  <pre class="code">[<span style="color: #2b91af">MetadataTypeAttribute</span>(<span style="color: blue">typeof</span>(<span style="color: #2b91af">Product</span>.<span style="color: #2b91af">ProductMetadata</span>))]
    <span style="color: blue">public partial class </span><span style="color: #2b91af">Product
    </span>{
        <span style="color: blue">internal sealed class </span><span style="color: #2b91af">ProductMetadata
        </span>{

            <span style="color: green">// Metadata classes are not meant to be instantiated.
            </span><span style="color: blue">private </span>ProductMetadata()
            {
            }

            <span style="color: blue">public int </span>Id { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

            [<span style="color: #2b91af">Display</span>(Name = <span style="color: #a31515">&quot;First Name&quot;</span>, Description = <span style="color: #a31515">&quot;Employee's first name&quot;</span>)] <span style="color: green">//Correct !
            //[DisplayName(&quot;First name 2&quot;)] // Wrong!
            </span><span style="color: blue">public string </span>Name { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

            <span style="color: blue">public </span><span style="color: #2b91af">EntityCollection</span>&lt;<span style="color: #2b91af">ProductTag</span>&gt; ProductTag { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        }
    }</pre>