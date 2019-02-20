---
ID: 3787
post_title: 'Fixing: TypeError: Cannot read property &#8216;sortable&#8217; of undefined, when using Kendo UI grid.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/05/22/fixing-typeerror-cannot-read-property-sortable-of-undefined-when-using-kendo-ui-grid/
published: true
post_date: 2014-05-22 15:21:27
---
<p>I was getting the error: TypeError: Cannot read property 'sortable' of undefined.</p>  <p>This was caused by dynamically changing Kendo UI grid columns, without destroying the grid first.</p>  <p>After I destroyed the grid and recreated it, the error was resolved.</p>  <p>To destroy a Kendo UI grid and later recreate it, use:</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: green">// Destroy kendo UI grid.
        // Must destroy and empty grid before refreshing columns.
        </span><span style="background: white; color: black">$(</span><span style="background: white; color: #a31515">'#crudGrid'</span><span style="background: white; color: black">).data().kendoGrid.destroy();
        $(</span><span style="background: white; color: #a31515">'#crudGrid'</span><span style="background: white; color: black">).empty();

        </span><span style="background: white; color: green">// Create Kendo UI grid.
        </span><span style="background: white; color: black">$(</span><span style="background: white; color: #a31515">'#crudGrid'</span><span style="background: white; color: black">).kendoGrid({
            dataSource: {
                data: products,
                schema: {
                    model: {
                        fields: {
                            ProductName: { type: </span><span style="background: white; color: #a31515">&quot;string&quot; </span><span style="background: white; color: black">},
                            UnitPrice: { type: </span><span style="background: white; color: #a31515">&quot;number&quot; </span><span style="background: white; color: black">},
                            UnitsInStock: { type: </span><span style="background: white; color: #a31515">&quot;number&quot; </span><span style="background: white; color: black">},
                            Discontinued: { type: </span><span style="background: white; color: #a31515">&quot;boolean&quot; </span><span style="background: white; color: black">}
                        }
                    }
                },
                pageSize: 20
            },
            height: 430,
            scrollable: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">,
            sortable: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">,
            filterable: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">,
            pageable: {
                input: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">,
                numeric: </span><span style="background: white; color: blue">false
            </span><span style="background: white; color: black">},
            columns: [
                </span><span style="background: white; color: #a31515">&quot;ProductName&quot;</span><span style="background: white; color: black">,
                { field: </span><span style="background: white; color: #a31515">&quot;UnitPrice&quot;</span><span style="background: white; color: black">, title: </span><span style="background: white; color: #a31515">&quot;Unit Price&quot;</span><span style="background: white; color: black">, format: </span><span style="background: white; color: #a31515">&quot;{0:c}&quot;</span><span style="background: white; color: black">, width: </span><span style="background: white; color: #a31515">&quot;130px&quot; </span><span style="background: white; color: black">},
                { field: </span><span style="background: white; color: #a31515">&quot;UnitsInStock&quot;</span><span style="background: white; color: black">, title: </span><span style="background: white; color: #a31515">&quot;Units In Stock&quot;</span><span style="background: white; color: black">, width: </span><span style="background: white; color: #a31515">&quot;130px&quot; </span><span style="background: white; color: black">},
                { field: </span><span style="background: white; color: #a31515">&quot;Discontinued&quot;</span><span style="background: white; color: black">, width: </span><span style="background: white; color: #a31515">&quot;130px&quot; </span><span style="background: white; color: black">}
            ]
        });</span></pre>