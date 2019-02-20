---
ID: 4856
post_title: CSS modules
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/04/07/css-modules/
published: true
post_date: 2016-04-07 07:40:35
---
<p>&nbsp;</p> <p>A great article on css modules: <a title="http://glenmaddern.com/articles/css-modules" href="http://glenmaddern.com/articles/css-modules">http://glenmaddern.com/articles/css-modules</a></p> <p>This allows css to be imported and used in JavaScript.</p> <p>A great fit for web components and can be easily used in frameworks like Aurelia, Angular, React etc.</p> <p>Example</p> <p><strong>CSS</strong></p> <p>Create a *.css file called submit-button.css&nbsp; with content:<br>.normal { /* all styles for Normal */ }<br>.disabled { /* all styles for Disabled */ }<br>.error { /* all styles for Error */ }<br>.inProgress { /* all styles for In Progress */</p> <p>&nbsp;</p> <p><strong>JavaScript</strong></p> <p>Then use the css in your JavaScript like:</p> <p>import styles from './submit-button.css';</p> <p>buttonElem.outerHTML = `&lt;button class=${styles.normal}&gt;Submit&lt;/button&gt;`</p> <p>&nbsp;</p> <p><strong>HTML (result)</strong></p> <p>&lt;button class="components_submit_button__normal__abc5436"&gt; Processing... &lt;/button&gt;</p> <p>&nbsp;</p> <p>Under the covers it uses ICSS, more on ICSS: <a title="http://glenmaddern.com/articles/interoperable-css" href="http://glenmaddern.com/articles/interoperable-css">http://glenmaddern.com/articles/interoperable-css</a></p>