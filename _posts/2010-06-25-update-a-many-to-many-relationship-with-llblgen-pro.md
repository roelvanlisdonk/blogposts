---
ID: 1570
post_title: >
  Update a many to many relationship with
  LLBLGen Pro and a ASP .NET DetailsView
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/25/update-a-many-to-many-relationship-with-llblgen-pro/
published: true
post_date: 2010-06-25 09:03:42
---
<p>If you have a database model like:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image21.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb21.png" width="754" height="402" /></a> </p>  <p>and you want to edit a CustomerEntity with LLGLGen Pro, before you save the CustomerEntity, you should delete all records in the table <strong>CustomerPermission</strong>.</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>Update a Customer</strong></p>  <p>The code is from a ASP .NET Webpage that uses a DetailsView to edit a Customer.<strong> </strong>It uses a CheckBoxList in the DetailsView to add and delete references between the table Customer and the table Permission.</p>  <pre class="code"><p><span style="color: blue">public void </span>Update_Click(<span style="color: blue">object </span>sender, <span style="color: #2b91af">DetailsViewUpdateEventArgs </span>e)
        {
            <span style="color: green">// Get the current CustomerId from the current URL
            </span><span style="color: blue">string </span>customerIdInQueryString = Request.QueryString[<span style="color: #a31515">&quot;CustomerId&quot;</span>];
            <span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(customerIdInQueryString))
            {
                <span style="color: green">// Only save or create a customer when a CustomerId is supplied in the URL
                </span><span style="color: blue">int </span>customerId = 0;
                <span style="color: blue">if </span>(<span style="color: blue">int</span>.TryParse(customerIdInQueryString, <span style="color: blue">out </span>customerId))
                {

                    <span style="color: #2b91af">CustomerEntity </span>customer = <span style="color: blue">new </span><span style="color: #2b91af">CustomerEntity</span>();
                    
                    <span style="color: green">// If customerId == -1 create a new customer, else edit an existing customer
                    </span><span style="color: blue">if </span>(customerId == -1) { customer.IsNew = <span style="color: blue">true</span>; } <span style="color: blue">else </span>{ customer.IsNew = <span style="color: blue">false</span>; }

                    <span style="color: green">// Set customer properties
                    </span>customer.Id = customerId;
                    customer .Name = e.NewValues[<span style="color: #a31515">&quot;Name&quot;</span>] == <span style="color: blue">null </span>? <span style="color: blue">null </span>: e.NewValues[<span style="color: #a31515">&quot;Naam&quot;</span>].ToString();
                    </p><p><span style="color: green">                    // Foreach item in the CheckBoxList that is selected create a reference from Customer to Permission </span>
                    <span style="color: #2b91af">CheckBoxList </span>cbl = (<span style="color: #2b91af">CheckBoxList</span>)<span style="color: blue">this</span>.customerDetailsView.FindControl(<span style="color: #a31515">&quot;PermissionCheckBoxList&quot;</span>);
                    customer.CustomerPermission.Clear();
                    <span style="color: blue">foreach </span>(<span style="color: #2b91af">ListItem </span>li <span style="color: blue">in </span>cbl.Items)
                    {
                        <span style="color: blue">if </span>(li.Selected)
                        {
                            <span style="color: #2b91af">CustomerPermissionEntity </span>spe = <span style="color: blue">new </span><span style="color: #2b91af">CustomerPermissionEntity</span>()
                            {
                                CustomerId = customer.Id,
                                PermissionId = <span style="color: blue">int</span>.Parse(li.Value)
                            };
                            customer.CustomerPermission.Add(spe);
                        }
                    }

                    this.UpdateCustomer(customer);

                    <span style="color: green">// Go back to overview page (containing a RadGrid)
                    </span>Response.Redirect(<span style="color: #a31515">&quot;CustomerOverview.aspx&quot;</span>);
                }
            }
        }
</p></pre>
<a href="http://11011.net/software/vspaste"></a>

<pre class="code"><span style="color: blue">private void </span>UpdateCustomer(<span style="color: #2b91af">Customerntity </span>customer)
        {
            <span style="color: blue">using </span>(<span style="color: blue">var </span>adapter = <span style="color: blue">new </span><span style="color: #2b91af">DataAccessAdapter</span>(ConfigurationManager.ConnectionStrings[<span style="color: #a31515">&quot;Main.ConnectionString&quot;</span>].ConnectionString))
            {
                <span style="color: green">// Delete entries in table CustomerPermission
                </span><span style="color: #2b91af">RelationPredicateBucket </span>bucket = <span style="color: blue">new </span><span style="color: #2b91af">RelationPredicateBucket</span>();
                bucket.PredicateExpression.Add(<span style="color: #2b91af">CustomerPermissionFields</span>.CustomerId == customer.Id);
                adapter.DeleteEntitiesDirectly(<span style="color: blue">typeof</span>(<span style="color: #2b91af">CustomePermissionEntity</span>), bucket);

                <span style="color: green">// Save Customer
                </span>adapter.SaveEntity(customer, <span style="color: blue">true</span>, <span style="color: blue">true</span>);
                adapter.CloseConnection();
            }
        }</pre>
<a href="http://11011.net/software/vspaste"></a>