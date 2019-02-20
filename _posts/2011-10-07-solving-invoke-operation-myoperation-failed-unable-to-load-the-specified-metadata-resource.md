---
ID: 2162
post_title: 'Solving: Invoke operation &#8216;MyOperation&#8217; failed. Unable to load the specified metadata resource.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/10/07/solving-invoke-operation-myoperation-failed-unable-to-load-the-specified-metadata-resource/
published: true
post_date: 2011-10-07 08:25:00
---
If you encounter the error: "Invoke operation 'MyOperation' failed. Unable to load the specified metadata resource". Please check the connection string used by Entity Framework.

In my case, I changed the namespace for the *.edmx file, but forgot to change the namespace in the connection string in the Web.config:

&nbsp;

I placed the *.edmx file in a folder Models en changed the namespace, so the following connection string was wrong:

&lt;add name="MyModel" connectionString="metadata=res://*/MyModel.csdl  ………………………

&nbsp;

<strong>Should be</strong>
&lt;add name="MyModel" connectionString="metadata=res://*/<strong>Models</strong>.MyModel.csdl ……………………………….

&nbsp;

<strong>StackTrace</strong>

at System.Data.Metadata.Edm.MetadataArtifactLoaderCompositeResource.LoadResources(String assemblyName, String resourceName, ICollection`1 uriRegistry, MetadataArtifactAssemblyResolver resolver)
at System.Data.Metadata.Edm.MetadataArtifactLoaderCompositeResource.CreateResourceLoader(String path, ExtensionCheck extensionCheck, String validExtension, ICollection`1 uriRegistry, MetadataArtifactAssemblyResolver resolver)
at System.Data.Metadata.Edm.MetadataArtifactLoader.Create(String path, ExtensionCheck extensionCheck, String validExtension, ICollection`1 uriRegistry, MetadataArtifactAssemblyResolver resolver)
at System.Data.Metadata.Edm.MetadataCache.SplitPaths(String paths)
at System.Data.Common.Utils.Memoizer`2.&lt;&gt;c__DisplayClass2.&lt;Evaluate&gt;b__0()
at System.Data.Common.Utils.Memoizer`2.Result.GetValue()
at System.Data.Common.Utils.Memoizer`2.Evaluate(TArg arg)
at System.Data.EntityClient.EntityConnection.GetMetadataWorkspace(Boolean initializeAllCollections)
at System.Data.Objects.ObjectContext.RetrieveMetadataWorkspaceFromConnection()
at System.Data.Objects.ObjectContext..ctor(EntityConnection connection, Boolean isConnectionConstructor)
at System.Data.Objects.ObjectContext..ctor(String connectionString, String defaultContainerName)

&nbsp;

An other create resource for resolving this problem is: http://blogs.teamb.com/craigstuntz/2010/08/13/38628/