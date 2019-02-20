---
ID: 4964
post_title: >
  Caculate trendline datapoints in
  TypeScript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/07/14/caculate-trendline-datapoints-in-typescript/
published: true
post_date: 2016-07-14 13:01:46
---
If you want to calculate trendline datapoints in TypeScript, you can use the following code:

&nbsp;

&nbsp;

&nbsp;
<h3>Code</h3>
&nbsp;

<pre>
<span style="color: blue; font-family: Courier New; font-size: 9pt;">module <span style="color: black;">helpers.math {</span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #a31515;">'use strict'<span style="color: black;">;</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: green;">/**<span style="color: black;">
</span></span></span><span style="color: green; font-family: Courier New; font-size: 9pt;"> * Based off: https://github.com/Tom-Alexander/regression-js/blob/master/src/regression.js<span style="color: black;">
</span></span><span style="color: green; font-family: Courier New; font-size: 9pt;"> * @param known_y - Array of numbers representing the y-axis values, [1, 2, ...].<span style="color: black;">
</span></span><span style="color: green; font-family: Courier New; font-size: 9pt;"> * @param known_x - Optional array of numbers representing the x-axis values, when not supplied this parameter will be [1,2,..."y-axis values total count"].<span style="color: black;">
</span></span><span style="color: green; font-family: Courier New; font-size: 9pt;"> */<span style="color: black;">
</span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">export <span style="color: black;"><span style="color: blue;">function<span style="color: black;"> trend(known_y: Array&lt;number&gt;, known_x?: Array&lt;number&gt;): Array&lt;number&gt; {
</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">const<span style="color: black;"> ylength = known_y.length;
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: green;">// When "x-axis values" are not supplied, generate it as [1,2,..."y-axis values total count"].<span style="color: black;">
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">if<span style="color: black;"> (!known_x) {
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">     known_x = [];
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">for<span style="color: black;"> (<span style="color: blue;">let<span style="color: black;"> xcounter = 0; xcounter &lt; ylength; xcounter++) {
</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">        known_x.push(xcounter + 1);
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">     }
</span><span style="color: black; font-family: Courier New; font-size: 9pt;"> }
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: green;">// The "data" should be in the format [[x[0], y[0]], [x[1], y[1]]], ...].<span style="color: black;">
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">const<span style="color: black;"> data = [];
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">for<span style="color: black;"> (<span style="color: blue;">let<span style="color: black;"> ycounter = 0; ycounter &lt; ylength; ycounter++) {
</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">     data.push([known_x[ycounter], known_y[ycounter]]);
</span><span style="color: black; font-family: Courier New; font-size: 9pt;"> }
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">let<span style="color: black;"> n = 0;
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">const<span style="color: black;"> results = [];</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">const<span style="color: black;"> sum = [0, 0, 0, 0, 0];</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">for<span style="color: black;"> (; n &lt; data.length; n++) {</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">if<span style="color: black;"> (data[n][1] != <span style="color: blue;">null<span style="color: black;">) {
</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">         sum[0] += data[n][0];
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">         sum[1] += data[n][1];
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">         sum[2] += data[n][0] * data[n][0];
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">         sum[3] += data[n][0] * data[n][1];
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">         sum[4] += data[n][1] * data[n][1];
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">     }
</span><span style="color: black; font-family: Courier New; font-size: 9pt;"> }
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">const<span style="color: black;"> gradient = (n * sum[3] - sum[0] * sum[1]) / (n * sum[2] - sum[0] * sum[0]);</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">const<span style="color: black;"> intercept = (sum[1] / n) - (gradient * sum[0]) / n;</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">for<span style="color: black;"> (<span style="color: blue;">let<span style="color: black;"> i = 0, len = data.length; i &lt; len; i++) {</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">const<span style="color: black;"> trendY = data[i][0] * gradient + intercept;
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">     results.push(trendY);
</span><span style="color: black; font-family: Courier New; font-size: 9pt;"> }
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">return<span style="color: black;"> results;
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;"> }
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">}
</span>
</pre>
&nbsp;

&nbsp;

&nbsp;
<h3>Unit Test</h3>
&nbsp;
<pre>
<span style="color: blue; font-family: Courier New; font-size: 9pt;">const<span style="color: black;"> trend = helpers.math.trend;
</span></span><span style="color: #a31515; font-family: Courier New; font-size: 9pt;">'use strict'<span style="color: black;">;
</span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">describe(<span style="color: #a31515;">'zvdz.helpers.calculate.trend'<span style="color: black;">, <span style="color: blue;">function<span style="color: black;"> () {
</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;"> it(<span style="color: #a31515;">'given an array of points it should return an array of points representing the trendline of the given points.'<span style="color: black;">, <span style="color: blue;">function<span style="color: black;"> () {
</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;"><span style="color: blue;">    const<span style="color: black;"> known_y = [1,2,3,4,5,6];
</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">     expect(trend(known_y)).toEqual([1, 2, 3, 4, 5, 6]);
</span><span style="color: black; font-family: Courier New; font-size: 9pt;"> });
</span><span style="color: black; font-family: Courier New; font-size: 9pt;">});
</span>
</pre>