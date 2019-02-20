---
ID: 5365
post_title: >
  Change linked service / dataset
  connection string in an Azure Data
  Factory with PowerShell after deployment
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2019/02/05/change-linked-service-dataset-connection-string-in-an-azure-data-factory-with-powershell-after-deployment/
published: true
post_date: 2019-02-05 17:56:12
---
<!-- wp:paragraph -->
<p>When you connect an Azure Data Factory to GIT it will create json files per linked service, but the json file will contain some part of the connection string. If you want to change the connection string after deployment, you can use the following script.</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>
# This script assumes the linked service json files can be found in the folder .\linkedService, relative to the location of this script.

param (
    [Parameter(Mandatory=$True)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$True)]
    [string]
    $DataFactoryName,

    [Parameter(Mandatory=$True)]
    [string]
    $Find,

    [Parameter(Mandatory=$True)]
    [string]
    $Replace
)

$root = $PSScriptRoot
$scriptName = $MyInvocation.MyCommand.Name
Write-Host "$scriptName - start"

Write-Host "Get all linked service json file names"
$linkedServicesPath = "$root\linkedService"
$names = Get-ChildItem -Path "$linkedServicesPath" -Name

Write-Host "Loop file names"
foreach ($name in $names)
{
    Write-Host "Find the text [$Find] and replace with [$Replace] in the file [$path]."
    $path = [System.IO.Path]::Combine($linkedServicesPath, $name)
    (Get-Content -Path "$path" -Raw).Replace("$Find", "$Replace") | Set-Content -Path "$path"

    $linkedServiceName = [System.IO.Path]::GetFileNameWithoutExtension($name)
    Write-Host "Update the linked service [$linkedServiceName] on ResourceGroupName [$ResourceGroupName] in DataFactoryName [$DataFactoryName] by using File [$path] on Azure.."
    Set-AzureRmDataFactoryV2LinkedService -ResourceGroupName "$ResourceGroupName" -DataFactoryName "$DataFactoryName" -Name "$linkedServiceName" -File "$path"
}

Write-Host "$scriptName - end"</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>Example linked service json file:<br>Note: The sql server database connections, that I use, use MSI for authentication.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>{
	"name": "MySqlDb1LinkedService",
	"type": "Microsoft.DataFactory/factories/linkedservices",
	"properties": {
		"type": "AzureSqlDatabase",
		"typeProperties": {
			"connectionString": "Integrated Security=False;Encrypt=True;Connection Timeout=30;Data Source=my-sql-server-v1.database.windows.net;Initial Catalog=MySqlDb1"
		}
	}
}</code></pre>
<!-- /wp:code -->