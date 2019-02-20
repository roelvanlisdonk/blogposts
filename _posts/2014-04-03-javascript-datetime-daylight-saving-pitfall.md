---
ID: 3718
post_title: >
  JavaScript DateTime daylight saving
  pitfall
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/04/03/javascript-datetime-daylight-saving-pitfall/
published: true
post_date: 2014-04-03 10:20:36
---
<p>Be aware, that dates with different daylight saving times, don’t differ by 24 hours per day, but 24 * days + 1 hour or 24 * days – 1 hour:</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">;

    </span><span style="background: white; color: green">// The &quot;main&quot; entry point for this application.
    </span><span style="background: white; color: black">self.start = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
    {
        console.log(</span><span style="background: white; color: #a31515">&quot;Document ready!&quot;</span><span style="background: white; color: black">);
        self.daylightSavingsTest();
    };

    self.daylightSavingsTest = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
    {
        </span><span style="background: white; color: green">// Notes (in the netherlands):
        // &quot;Winter time&quot; refers to &quot;standard time&quot;.
        // &quot;Summer time&quot; refers to &quot;standard time&quot; + 1 hour.
        // Time changes at sunday [2014-03-30: 02:00:00.000]. Changes to [2014-03-30: 03:00:00.000]. 
        
        
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">d1 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Date(2014, 1, 1, 0, 0, 0, 0); </span><span style="background: white; color: green">// '2014-02-01: 00:00:00.000';
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">d2 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Date(2014, 1, 3, 0, 0, 0, 0); </span><span style="background: white; color: green">// '2014-02-03: 00:00:00.000';

        // [getTime()], returns the number of milliseconds since [1970-01-01 00:00:00] (winter / standard time).
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">t1 = d1.getTime();
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">t2 = d2.getTime();

        </span><span style="background: white; color: green">// When all daylight saving times of 2 dates are the same, 
        // you can calculate the difference in days between 2 dates with parseInt((t2 - t1) / (24 * 60 * 60 * 1000)):
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">days = parseInt((t2 - t1) / (24 * 60 * 60 * 1000));
        console.log(days); </span><span style="background: white; color: green">// Outputs: 2

        // When all daylight saving times of 2 dates are NOT the same, 
        // you can't calculate the difference in days between 2 dates with parseInt((t2 - t1) / (24 * 60 * 60 * 1000)):
        </span><span style="background: white; color: black">d1 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Date(2014, 2, 30, 0, 0, 0, 0); </span><span style="background: white; color: green">// '2014-03-30: 00:00:00.000';
        </span><span style="background: white; color: black">d2 = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Date(2014, 3, 1, 0, 0, 0, 0);  </span><span style="background: white; color: green">// '2014-04-01: 00:00:00.000';
        </span><span style="background: white; color: black">t1 = d1.getTime();
        t2 = d2.getTime();
        days = parseInt((t2 - t1) / (24 * 60 * 60 * 1000));
        console.log(days); </span><span style="background: white; color: green">// Outputs: 1

        // You can fix this by using Math.round:
        </span><span style="background: white; color: black">days = Math.round((t2 - t1) / (24 * 60 * 60 * 1000));
        console.log(days); </span><span style="background: white; color: green">// Outputs: 2


        // Or just use moment.js!!!!

    </span><span style="background: white; color: black">};

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
})();

</span><span style="background: white; color: green">// Start the application.
</span><span style="background: white; color: black">app.start();</span></pre>


<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/04/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/04/image_thumb.png" width="244" height="90" /></a></p>