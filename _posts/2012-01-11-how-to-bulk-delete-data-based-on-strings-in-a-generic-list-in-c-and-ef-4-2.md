---
ID: 2454
post_title: 'How to bulk delete data based on strings in a generic list in C# and EF 4.2'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/01/11/how-to-bulk-delete-data-based-on-strings-in-a-generic-list-in-c-and-ef-4-2/
published: true
post_date: 2012-01-11 14:32:27
---
<p>Let’s assume you have a table Customer in a Microsoft SQL Server database:</p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/01/image50.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/01/image_thumb50.png" width="580" height="364"></a></p> <p>&nbsp;</p> <p>And want to delete Customer_008, Customer_009, Customer_010, Customer_011 based on a generic list in C#, you can join this generic list with a entity dbset in entityframework 4.2:</p> <p>NOTE: For best performance start the query with the generic list and then join on the Customer table.</p> <p>&nbsp;</p><pre class="code">[<span style="color: #2b91af">TestMethod</span>]
<span style="color: blue">public void </span>RunNewCodeTest()
{
    TestBulkDelete();
}

<span style="color: blue">private void </span>TestBulkDelete()
{
    <span style="color: green">// Define customers to delete in a generic list of strings.
    </span><span style="color: blue">var </span>names = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt;();
    names.Add(<span style="color: #a31515">"Customer_038"</span>);
    names.Add(<span style="color: #a31515">"Customer_039"</span>);
    names.Add(<span style="color: #a31515">"Customer_040"</span>);
    names.Add(<span style="color: #a31515">"Customer_041"</span>);

    <span style="color: blue">using </span>(<span style="color: blue">var </span>entities = <span style="color: blue">new </span>Rvl.NewCode.Model.<span style="color: #2b91af">NewCodeEntities</span>())
    {
        <span style="color: green">// To improve performance by a factor 1000, set Configuration.AutoDetectChangesEnabled = false.
        </span>entities.Configuration.AutoDetectChangesEnabled = <span style="color: blue">false</span>;

        <span style="color: green">// Get customers to delete.
        </span><span style="color: blue">var </span>query = <span style="color: blue">from </span>name <span style="color: blue">in </span>names
                    <span style="color: blue">join </span>customer <span style="color: blue">in </span>entities.Customer <span style="color: blue">on </span>name <span style="color: blue">equals </span>customer.Name
                    <span style="color: blue">select </span>customer;
        <span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Customer</span>&gt; customersToDelete = query.ToList();

        <span style="color: green">// Delete customers from context.
        </span><span style="color: blue">foreach </span>(<span style="color: #2b91af">Customer </span>customer <span style="color: blue">in </span>customersToDelete)
        {
            entities.Customer.Remove(customer);
        }

        <span style="color: green">// Delete customers from database.
        </span>entities.SaveChanges();
    }
}
</pre>
<p>&nbsp;</p>
<p>&nbsp;</p><pre class="code"></pre>