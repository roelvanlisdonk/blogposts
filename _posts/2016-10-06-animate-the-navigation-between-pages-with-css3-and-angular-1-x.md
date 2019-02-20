---
ID: 5007
post_title: >
  Animate the navigation between pages
  with CSS3 and Angular 1.x
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/10/06/animate-the-navigation-between-pages-with-css3-and-angular-1-x/
published: true
post_date: 2016-10-06 22:11:15
---
<pre>
Just created a code pen to demonstrate the navigation between pages in Angular 1.x by using css3.

The animation should mimic scrolling the pages from top to bottom, now I could have just&#160; used TypeScript,
to calculate the correct scroll position, but in this case I wanted to use pure CSS3.

I had some difficulties to create this animation, because my first reaction was, to try and use ng-if or 
ng-show / ng-hide, to hide the pages that are not visible. After hours of trying, I did not succeed, 
so I tried a different approach, by stacking the pages on top of each other and moving “previous pages” 
outside of the list at the top and moving next pages outside of the list at the bottom, without using 
ng-if or ng-hide.

Note:
- by using a translateX you could make the pages scroll from left to right instead of from bottom to top.
- by switching the values for translateY, you could make the pages scroll from top to bottom.

<a title="http://codepen.io/roelvanlisdonk/pen/YGZqgO/" href="http://codepen.io/roelvanlisdonk/pen/YGZqgO/">http://codepen.io/roelvanlisdonk/pen/YGZqgO/&quot;</a>


<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/10/image-2.png" rel="lightbox"><img title="image" style="display: inline; background-image: none;" border="0" alt="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/10/image_thumb-2.png" width="611" height="297" /></a>
</pre>