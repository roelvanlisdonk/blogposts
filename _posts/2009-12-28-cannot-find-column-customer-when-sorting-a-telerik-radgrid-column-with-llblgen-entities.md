---
ID: 887
post_title: >
  Cannot find column Customer when sorting
  a Telerik RadGrid column with LLBLGen
  entities
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/28/cannot-find-column-customer-when-sorting-a-telerik-radgrid-column-with-llblgen-entities/
published: true
post_date: 2009-12-28 09:31:03
---
<p>When you sort a column in a Telerik RadGrid you get the error “Cannot find column Customer”, make sure the&#160; <strong>SortExpression</strong> is the same as the <strong>DataField</strong></p>  <pre class="code"><span style="color: red">                   DataField</span><span style="color: blue">=&quot;Customer.Description&quot;
                   </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;Customer&quot;
                   </span><span style="color: red">SortExpression</span><span style="color: blue">=&quot;Customer.Description&quot;
                   </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;Customer&quot; </span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br />If SortExpression is not the same as the DataFiel, you will get the error:

  <br /></p>

<p><b>Message</b>: <b>Cannot find column Customer</b>

  <br /><b>Exception</b>: System.IndexOutOfRangeException

  <br /><b>Targetsite</b>: System.Data.IndexField[] ParseSortString(System.String)

  <br /><b>Source</b>: System.Data

  <br /><b>StackTrace</b>: at System.Data.DataTable.ParseSortString(String sortString)

  <br />at System.Data.DataView.CheckSort(String sort)

  <br />at System.Data.DataView.set_Sort(String value)

  <br />at Telerik.Web.UI.GridEnumerableFromDataView.PerformTransformation()

  <br />at Telerik.Web.UI.GridEnumerableFromDataView.TransformEnumerable()

  <br />at Telerik.Web.UI.GridTableView.GetEnumerator(Boolean useDataSource, GridEnumerableBase resolvedDataSource, ArrayList dataKeysArray)

  <br />at Telerik.Web.UI.GridTableView.CreateControlHierarchy(Boolean useDataSource)

  <br />at Telerik.Web.UI.GridTableView.CreateChildControls(IEnumerable dataSource, Boolean useDataSource)

  <br />at System.Web.UI.WebControls.CompositeDataBoundControl.PerformDataBinding(IEnumerable data)

  <br />at System.Web.UI.WebControls.DataBoundControl.OnDataSourceViewSelectCallback(IEnumerable data)

  <br />at System.Web.UI.DataSourceView.Select(DataSourceSelectArguments arguments, DataSourceViewSelectCallback callback)

  <br />at System.Web.UI.WebControls.DataBoundControl.PerformSelect()

  <br />at Telerik.Web.UI.GridTableView.PerformSelect()

  <br />at System.Web.UI.WebControls.BaseDataBoundControl.DataBind()

  <br />at Telerik.Web.UI.GridTableView.DataBind()

  <br />at Telerik.Web.UI.GridSortCommandEventArgs.ExecuteCommand(Object source)

  <br />at Telerik.Web.UI.RadGrid.OnBubbleEvent(Object source, EventArgs e)

  <br />at System.Web.UI.Control.RaiseBubbleEvent(Object source, EventArgs args)

  <br />at Telerik.Web.UI.GridItem.OnBubbleEvent(Object source, EventArgs e)

  <br />at System.Web.UI.Control.RaiseBubbleEvent(Object source, EventArgs args)

  <br />at Telerik.Web.UI.GridItem.OnBubbleEvent(Object source, EventArgs e)

  <br />at System.Web.UI.Control.RaiseBubbleEvent(Object source, EventArgs args)

  <br />at System.Web.UI.WebControls.LinkButton.OnCommand(CommandEventArgs e)

  <br />at System.Web.UI.WebControls.LinkButton.RaisePostBackEvent(String eventArgument)

  <br />at System.Web.UI.WebControls.LinkButton.System.Web.UI.IPostBackEventHandler.RaisePostBackEvent(String eventArgument)

  <br />at System.Web.UI.Page.RaisePostBackEvent(IPostBackEventHandler sourceControl, String eventArgument)

  <br />at System.Web.UI.Page.RaisePostBackEvent(NameValueCollection postData)

  <br />at System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint)

  <br /><b>Data count</b>: 0</p>