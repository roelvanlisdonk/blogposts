---
ID: 4152
post_title: >
  Setting height / width sparklines and
  removing spacing with Kendo UI and
  AngularJS
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/11/19/setting-height-width-sparklines-and-removing-spacing-with-kendo-ui-and-angularjs/
published: true
post_date: 2014-11-19 14:39:46
---
<p>In the following screendump, I used 6 sparkline fields:</p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image7.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image_thumb7.png" width="580" height="114"></a></p> <p>&nbsp;</p> <p>To increase the width / height of the sparkline (bar) I set the following values:</p> <p>- charArea options (height, padding, margin)</p> <p>- Series options (gap and spacing)</p><pre class="code"><span style="background: white; color: black">$scope.kostenMinderPersoneelChartOptions = {
            chartArea: {
                background: </span><span style="background: white; color: #a31515">""</span><span style="background: white; color: black">,
                height: 17,
                margin: {
                    top: 1,
                    bottom: 0,
                    left: 0,
                    right: 0
                },
                padding: 0
            },
            tooltip: {
                visible: </span><span style="background: white; color: blue">false
            </span><span style="background: white; color: black">},
            series: [
                {
                    type: </span><span style="background: white; color: #a31515">'bar'</span><span style="background: white; color: black">,
                    color: </span><span style="background: white; color: #a31515">'#EC008C'</span><span style="background: white; color: black">,
                    field: </span><span style="background: white; color: #a31515">'sparkline'</span><span style="background: white; color: black">,
                    gap: 0,
                    spacing: 0
                }
            ],
            valueAxis: {
                min: 0,
                max: 200000
            }
        };</span></pre><pre class="code"></pre>