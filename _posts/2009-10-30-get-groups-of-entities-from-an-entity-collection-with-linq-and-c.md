---
ID: 782
post_title: 'Get groups of entities from an entity collection with Linq and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/30/get-groups-of-entities-from-an-entity-collection-with-linq-and-c/
published: true
post_date: 2009-10-30 12:05:00
---
<p>If you want to get groups of entities from an entitycollection in C# you can use Linq:    <br /></p>  <p><strong>Assignment class</strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;

<span style="color: blue">namespace </span>Rvl.HelperTools.Common.BE
{
    <span style="color: blue">public class </span><span style="color: #2b91af">Assignment
    </span>{
        <span style="color: blue">public </span><span style="color: #2b91af">DateTime </span>Startdate { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public </span><span style="color: #2b91af">DateTime </span>Enddate { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>Customername { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    }
}</pre>

<p><strong>Create function</strong></p>
<a href="http://11011.net/software/vspaste"></a>

<div align="left">
  <pre class="code"><span style="color: blue">        public void </span>CreateGroupsOfEntitiesFromEntityCollection()
        {
            <span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Assignment</span>&gt; sourceAssignments = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Assignment</span>&gt;()
            {
                <span style="color: blue">new </span><span style="color: #2b91af">Assignment</span>() { Startdate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(1), Enddate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(2), Customername = <span style="color: #a31515">&quot;Microsoft&quot; </span>},
                <span style="color: blue">new </span><span style="color: #2b91af">Assignment</span>() { Startdate = <span style="color: #2b91af">DateTime</span>.Now, Enddate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(1), Customername = <span style="color: #a31515">&quot;Microsoft&quot; </span>},
                <span style="color: blue">new </span><span style="color: #2b91af">Assignment</span>() { Startdate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(1), Enddate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(2), Customername = <span style="color: #a31515">&quot;IBM&quot; </span>},
                <span style="color: blue">new </span><span style="color: #2b91af">Assignment</span>() { Startdate = <span style="color: #2b91af">DateTime</span>.Now, Enddate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(1), Customername = <span style="color: #a31515">&quot;IBM&quot; </span>},
                <span style="color: blue">new </span><span style="color: #2b91af">Assignment</span>() { Startdate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(1), Enddate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(2), Customername = <span style="color: #a31515">&quot;Google&quot; </span>},
                <span style="color: blue">new </span><span style="color: #2b91af">Assignment</span>() { Startdate = <span style="color: #2b91af">DateTime</span>.Now, Enddate = <span style="color: #2b91af">DateTime</span>.Now.AddDays(1), Customername = <span style="color: #a31515">&quot;Google&quot; </span>}
            };

            <span style="color: blue">var </span>assignmentGroups = <span style="color: blue">from </span>a <span style="color: blue">in </span>sourceAssignments
                                   <span style="color: blue">orderby </span>a.Customername, a.Startdate
                                   <span style="color: blue">group </span>a <span style="color: blue">by </span>a.Customername <span style="color: blue">into </span>g <span style="color: blue">select new </span>{ Customername = g.Key, Assignments = g };

            <span style="color: blue">foreach </span>(<span style="color: blue">var </span>g <span style="color: blue">in </span>assignmentGroups)
            {
                <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Customername {0}&quot;</span>, g.Customername));
                <span style="color: blue">foreach </span>(<span style="color: blue">var </span>a <span style="color: blue">in </span>g.Assignments)
                {
                    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Assignment startdate {0}&quot;</span>, a.Startdate));
                }
            }
        }</pre>
  <a href="http://11011.net/software/vspaste"></a></div>
<a href="http://11011.net/software/vspaste"></a>

<p><strong></strong></p>

<p><strong>Result
    <br /></strong></p>

<p>Customername Google
  <br />Assignment startdate 30-10-2009 11:17:47

  <br />Assignment startdate 31-10-2009 11:17:47

  <br />Customername IBM

  <br />Assignment startdate 30-10-2009 11:17:47

  <br />Assignment startdate 31-10-2009 11:17:47

  <br />Customername Microsoft

  <br />Assignment startdate 30-10-2009 11:17:47

  <br />Assignment startdate 31-10-2009 11:17:47</p>