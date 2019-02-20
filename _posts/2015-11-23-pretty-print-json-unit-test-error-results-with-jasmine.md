---
ID: 4673
post_title: >
  Pretty print json unit test error
  results with Jasmine
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/11/23/pretty-print-json-unit-test-error-results-with-jasmine/
published: true
post_date: 2015-11-23 14:51:40
---
<p>&#160;</p>  <p>&#160;</p>  <p>&#160;</p>  <p>If you use the standard HTML reporter for jasmine an expect like:</p>  <p><font color="#9b00d3">expect(JSON.stringify(actual)).toEqual(JSON.stringify(expected));</font></p>  <p>would result in:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/11/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/11/image_thumb.png" width="580" height="182" /></a></p>    <p>If you replace the div tag with a pre tag in the “jasmine-html.js” file.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/11/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/11/image_thumb1.png" width="580" height="88" /></a></p>  <p>&#160;</p>  <p>&#160;</p>  <p>and use the third paramater of the JSON.stringify method to pretty print the JSON, </p>  <p>like: </p>  <p><font color="#9b00d3">expect(JSON.stringify(actual, null, 4)).toEqual(JSON.stringify(expected, null, 4));</font></p>  <p>&#160;</p>  <p>the result will be:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/11/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/11/image_thumb2.png" width="219" height="625" /></a></p>  <p>&#160;</p>  <p>In some cases this will simplify, spotting the error in the JSON result.</p>