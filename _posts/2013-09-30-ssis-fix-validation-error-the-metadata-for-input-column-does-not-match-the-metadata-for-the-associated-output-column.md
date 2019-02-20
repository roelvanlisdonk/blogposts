---
ID: 3453
post_title: 'SSIS Fix: Validation error. The metadata for input column &ldquo;&hellip;..&rdquo; does not match the metadata for the associated output column.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/09/30/ssis-fix-validation-error-the-metadata-for-input-column-does-not-match-the-metadata-for-the-associated-output-column/
published: true
post_date: 2013-09-30 14:02:21
---
<p>&#160;</p>  <p>After a schema change in the database I got the error: The metadata for input column “…..” does not match the metadata for the associated output column, on a Union all data flow transformation. To fix this problem:</p>  <p>Right click the &quot;Union All&quot;&#160; &gt; Edit…</p>  <p>Change the &quot;Union All Input 2&quot; value for the specific column to &lt;ignore&gt;:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image21.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb21.png" width="580" height="153" /></a></p>  <p>&#160;</p>  <p>Click on OK</p>  <p>Save package</p>  <p>Right click again on the &quot;Union All&quot;&#160; &gt; Edit…</p>  <p>Change the &quot;Union All Input 2&quot; value for the specific column to the correct value:</p>  <p>Click on OK</p>  <p>Save package</p>  <p>The error should be fixed.</p>