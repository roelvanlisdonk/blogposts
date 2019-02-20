---
ID: 2838
post_title: 'How to fix: Count on a group by in LINQ returns 1, when used in a left outer join.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/09/26/how-to-fix-count-on-a-group-by-in-linq-returns-1-when-used-in-a-left-outer-join/
published: true
post_date: 2012-09-26 16:07:00
---
<p>If you do a count on a group by in LINQ when using a left outer join, the count will be 1 even though there are no records found for the group. This is caused by the DefaultIfEmpty. The DefaultIfEmpty will insert 1 default object for each group that does not contain any records.</p>  <p>To fix this, adjust the Count, so it ignores the inserted default objects:</p>   <p>&#160;</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;
<span style="color: blue">using </span>System.Collections.Generic;

<span style="color: blue">namespace </span>Research.Rli.Tests
{
   
    [<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">ResearchTester
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>Count_should_be_zero_when_left_outer_join_contains_no_values()
        {
            <span style="color: blue">var </span>statussen = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">StatusDto</span>&gt; 
            { 
                <span style="color: blue">new </span><span style="color: #2b91af">StatusDto </span>{ Id = 0 }, 
                <span style="color: blue">new </span><span style="color: #2b91af">StatusDto </span>{ Id = 1 }, 
                <span style="color: blue">new </span><span style="color: #2b91af">StatusDto </span>{ Id = 2 } 
            };
            <span style="color: blue">var </span>actualAlerts = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">RecordDto</span>&gt; 
            { 
                <span style="color: blue">new </span><span style="color: #2b91af">RecordDto </span>{ Id = 1, StatusId = 2 }, 
                <span style="color: blue">new </span><span style="color: #2b91af">RecordDto </span>{ Id = 2, StatusId = 2 }, 
                <span style="color: blue">new </span><span style="color: #2b91af">RecordDto </span>{ Id = 3, StatusId = 2 }, 
                <span style="color: blue">new </span><span style="color: #2b91af">RecordDto </span>{ Id = 4, StatusId = 2 } 
            };

            <font color="#ff0000"><font size="2"><span style="color: blue">int </span>defaultRecordId = -2;</font></font>
            <span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">ResultDto</span>&gt; totals = (<span style="color: blue">from </span>s <span style="color: blue">in </span>statussen
                                      <span style="color: blue">join </span>aa <span style="color: blue">in </span>actualAlerts <span style="color: blue">on </span>s.Id <span style="color: blue">equals </span>aa.StatusId <span style="color: blue">into </span>gaa
                                      <span style="color: blue">from </span>aaEmpty <span style="color: blue">in </span><font color="#ff0000">gaa.DefaultIfEmpty(<span style="color: blue">new </span><span style="color: #2b91af">RecordDto </span>{ Id = defaultRecordId })</font>
                                      <span style="color: blue">group </span>aaEmpty <span style="color: blue">by </span>s.Id <span style="color: blue">into </span>grp
                                      <span style="color: blue">select new </span><span style="color: #2b91af">ResultDto 
                                                </span>{ 
                                                    StatusId = grp.Key, 
                                                    <font color="#ff0000" size="2">Count = grp.Count(x =&gt; x.Id != defaultRecordId)</font> 
                                                }).ToList();

            <span style="color: #2b91af">Assert</span>.AreEqual(0, totals[0].Count);
            <span style="color: #2b91af">Assert</span>.AreEqual(0, totals[1].Count);
            <span style="color: #2b91af">Assert</span>.AreEqual(4, totals[2].Count);

        }
    }
    <span style="color: blue">public class </span><span style="color: #2b91af">RecordDto
    </span>{
        <span style="color: blue">public int </span>Id { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public int </span>StatusId { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    }
    <span style="color: blue">public class </span><span style="color: #2b91af">StatusDto
    </span>{
        <span style="color: blue">public int </span>Id { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    }
    <span style="color: blue">public class </span><span style="color: #2b91af">ResultDto
    </span>{
        <span style="color: blue">public int </span>StatusId { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public int </span>Count { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    }
}</pre>