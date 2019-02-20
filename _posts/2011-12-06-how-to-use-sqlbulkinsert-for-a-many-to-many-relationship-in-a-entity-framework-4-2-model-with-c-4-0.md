---
ID: 2266
post_title: 'How to use SqlBulkInsert for a many to many relationship in a Entity Framework 4.2 model with C# 4.0'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/06/how-to-use-sqlbulkinsert-for-a-many-to-many-relationship-in-a-entity-framework-4-2-model-with-c-4-0/
published: true
post_date: 2011-12-06 11:09:29
---
<p>Let’s say your product has a many to many relation between products en customers, then the the Entity Framework 4.2 model would look like:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb.png" width="580" height="239" /></a></p>  <p>&#160;</p>  <p>A night process imports customers and the products they bought into a reporting database. During the night process the reporting database is closed, so we can lock the tables, then you can use the following C# code to insert data:</p>  <p>&#160;</p>  <p><strong><font size="4">Result</font></strong></p>  <p>Inserting 1.000 products, 1.000 customers and <strong>1.000.000 sales records</strong> takes about <strong>42 seconds</strong> on my laptop</p>  <p>Laptop cpu utilization:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image1.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb1.png" width="558" height="487" /></a></p>  <p>&#160;</p>  <p>Laptop disk utilization:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image2.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb2.png" width="580" height="33" /></a></p>  <p>&#160;</p>  <p>If you would use Entity Framework to insert, then this would take fore ever <img style="border-bottom-style: none; border-left-style: none; border-top-style: none; border-right-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Winking smile" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/wlEmoticon-winkingsmile.png" /></p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong><font size="4">Code</font></strong></p>  <p><strong>The code could use the entity framework 4.2 entities and the data annotations applied to those entities, to validate the data to insert. That will be explained in an other post.</strong> The code uses one transaction to put all the data in the database and it will lock the tables to get a continuous identity on the tables. When an exceptions occurs the transaction will be roll backed.</p>  <p>&#160;</p>  <pre class="code">[<span style="color: #2b91af">TestMethod</span>]
<span style="color: blue">public void </span>TestMethod1()
{
    BulkInsertManyToManyRelationship();
}
<span style="color: blue">public void </span>BulkInsertManyToManyRelationship()
{
    <span style="color: green">// Connect to the database.
    </span><span style="color: blue">using </span>(<span style="color: blue">var </span>connection = <span style="color: blue">new </span><span style="color: #2b91af">SqlConnection</span>(<span style="color: #a31515">&quot;data source=.;initial catalog=Research;integrated security=True;multipleactiveresultsets=True;&quot;</span>))
    {
        connection.Open();

        <span style="color: #2b91af">SqlTransaction </span>transaction = <span style="color: blue">null</span>;
        <span style="color: #2b91af">DataTable </span>productTable = <span style="color: blue">null</span>;
        <span style="color: #2b91af">DataTable </span>customerTable = <span style="color: blue">null</span>;
        <span style="color: #2b91af">DataTable </span>saleTable = <span style="color: blue">null</span>;
        <span style="color: blue">try
        </span>{
            transaction = connection.BeginTransaction(); <span style="color: green">// Use one transaction to put all the data in the database

            // Create 1.000 products.
            </span><span style="color: blue">int </span>lastProductIdentity = 0;
            <span style="color: blue">int </span>productCount = 1000;
            <span style="color: blue">string </span>productTableName = <span style="color: #a31515">&quot;Product&quot;</span>;
            productTable = GetSchemaInfo(productTableName, connection, transaction);
            <span style="color: blue">for </span>(<span style="color: blue">int </span>i = 0; i &lt; productCount; i++) 
            {
                <span style="color: #2b91af">DataRow </span>row = productTable.NewRow();
                row[1] = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}_{1}&quot;</span>, productTableName, i.ToString().PadLeft(3, <span style="color: #a31515">'0'</span>));
                productTable.Rows.Add(row);
            }
            BulkInsertTable(productTableName, productTable, connection, transaction);
            lastProductIdentity = GetIdentity(productTableName, connection, transaction);


            <span style="color: green">// Create 1.000 customers.
            </span><span style="color: blue">int </span>lastCustomerIdentity = 0;
            <span style="color: blue">int </span>customerCount = 1000;
            <span style="color: blue">string </span>customerTableName = <span style="color: #a31515">&quot;Customer&quot;</span>;
            customerTable = GetSchemaInfo(customerTableName, connection, transaction);
            <span style="color: blue">for </span>(<span style="color: blue">int </span>i = 0; i &lt; customerCount; i++) 
            {
                <span style="color: #2b91af">DataRow </span>row = customerTable.NewRow();
                row[1] = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}_{1}&quot;</span>, customerTableName, i.ToString().PadLeft(3, <span style="color: #a31515">'0'</span>));
                customerTable.Rows.Add(row);
            }
            BulkInsertTable(customerTableName, customerTable, connection, transaction);
            lastCustomerIdentity = GetIdentity(customerTableName, connection, transaction);


            <span style="color: green">// Add all products to all customers, this will create 1.000.000 records
            </span><span style="color: blue">string </span>saleTableName = <span style="color: #a31515">&quot;Sale&quot;</span>;
            saleTable = GetSchemaInfo(saleTableName, connection, transaction);
            <span style="color: blue">for </span>(<span style="color: blue">int </span>c = lastCustomerIdentity - customerCount; c &lt; lastCustomerIdentity; c++)
            {
                <span style="color: blue">for </span>(<span style="color: blue">int </span>p = lastProductIdentity - productCount; p &lt; lastProductIdentity; p++)
                {
                    <span style="color: #2b91af">DataRow </span>row = saleTable.NewRow();
                    row[1] = p;
                    row[2] = c;
                    saleTable.Rows.Add(row);
                }
            }
            BulkInsertTable(saleTableName, saleTable, connection, transaction);

            transaction.Commit();
        }
        <span style="color: blue">catch</span>(<span style="color: #2b91af">Exception </span>ex)
        {
            transaction.Rollback(); <span style="color: green">// This will not reset IDENT_CURRENT
        </span>}
        <span style="color: blue">finally
        </span>{
            <span style="color: blue">if </span>(productTable != <span style="color: blue">null</span>) { productTable.Dispose(); }
            <span style="color: blue">if </span>(customerTable != <span style="color: blue">null</span>) { customerTable.Dispose(); }
            <span style="color: blue">if </span>(saleTable != <span style="color: blue">null</span>) { saleTable.Dispose(); }
            <span style="color: blue">if </span>(transaction != <span style="color: blue">null</span>) { transaction.Dispose(); }
        }
    }
}
<span style="color: blue">public </span><span style="color: #2b91af">DataTable </span>GetSchemaInfo(<span style="color: blue">string </span>tableName, <span style="color: #2b91af">SqlConnection </span>connection, <span style="color: #2b91af">SqlTransaction </span>transaction)
{
    <span style="color: #2b91af">DataTable </span>dataTable = <span style="color: blue">new </span><span style="color: #2b91af">DataTable</span>();
    <span style="color: blue">using </span>(<span style="color: #2b91af">SqlCommand </span>selectSchemaCommand = connection.CreateCommand())
    {
        selectSchemaCommand.CommandText = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;set fmtonly on; select * from {0}&quot;</span>, tableName);
        selectSchemaCommand.Transaction = transaction;

        <span style="color: blue">using </span>(<span style="color: blue">var </span>adapter = <span style="color: blue">new </span><span style="color: #2b91af">SqlDataAdapter</span>(selectSchemaCommand)) <span style="color: green">// Get only the schema information for table [Sale]
        </span>{
            adapter.FillSchema(dataTable, <span style="color: #2b91af">SchemaType</span>.Source);
        }
    }
    <span style="color: blue">return </span>dataTable;
}
<span style="color: blue">public int </span>GetIdentity(<span style="color: blue">string </span>tableName, <span style="color: #2b91af">SqlConnection </span>connection, <span style="color: #2b91af">SqlTransaction </span>transaction)
{
    <span style="color: blue">int </span>identity = 0;

    <span style="color: green">// Get the last customer identity
    </span><span style="color: blue">using </span>(<span style="color: #2b91af">SqlCommand </span>sqlCommand = connection.CreateCommand())
    {
        sqlCommand.CommandText = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;SELECT IDENT_CURRENT('{0}')&quot;</span>, tableName);
        sqlCommand.Transaction = transaction;
        identity = <span style="color: #2b91af">Convert</span>.ToInt32(sqlCommand.ExecuteScalar());
    }

    <span style="color: blue">return </span>identity;
}
<span style="color: blue">public void </span>BulkInsertTable(<span style="color: blue">string </span>tableName, <span style="color: #2b91af">DataTable </span>dataTable, <span style="color: #2b91af">SqlConnection </span>connection, <span style="color: #2b91af">SqlTransaction </span>transaction)
{
    <span style="color: blue">using </span>(<span style="color: blue">var </span>sqlBulkCopy = <span style="color: blue">new </span><span style="color: #2b91af">SqlBulkCopy</span>(connection, <span style="color: #2b91af">SqlBulkCopyOptions</span>.TableLock, transaction)) <span style="color: green">// Lock the table
    </span>{
        sqlBulkCopy.DestinationTableName = tableName;
        sqlBulkCopy.WriteToServer(dataTable);
    }
}</pre>