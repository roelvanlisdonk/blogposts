---
ID: 5255
post_title: 'Fix: Power BI POST request returns a 500 Internal Server Error'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/10/05/fix-power-bi-post-request-returns-a-500-internal-server-error/
published: true
post_date: 2018-10-05 13:40:28
---
<p>When posting to the Power BI api uri: <a href="https://api.powerbi.com/v1.0/myorg/groups">https://api.powerbi.com/v1.0/myorg/groups</a> in PowerShell version 5.1.17134.228, I got the error:
</p><p><strong>The remote server returned an error: (500) Internal Server Error.
</strong></p><p>
 </p><p>I invoked the Power BI rest api with the PowerShell script you can find below.
</p><p>The error was fixed, when I added -ContentType 'application/json' parameter to the InvokeRestMethod
</p><p>
 </p><p>
 </p><p><strong>PowerShell script
</strong></p><p>
 </p><p>       $clientId = "my-client-id"
</p><p>        $PowerBIUserName = "MyUserName"
</p><p>        $PowerBIUserPassword = "MyUserPassword"
</p><p>        $creds = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.UserCredential" -ArgumentList $PowerBIUserName,$PowerBIUserPassword
</p><p>        $resourceAppIdURI = "https://analysis.windows.net/powerbi/api"
</p><p>        $authority = "https://login.microsoftonline.com/common/oauth2/authorize";
</p><p>        $authContext = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext" -ArgumentList $authority
</p><p>
 </p><p>        # Acquire token
</p><p>        $authResult = $authContext.AcquireToken($resourceAppIdURI, $clientId, $creds)
</p><p>
 </p><p>        # Create a new group
</p><p>        $auth_header = @{
</p><p>            'Authorization'=$token.CreateAuthorizationHeader()
</p><p>        }
</p><p>        $uri = "https://api.powerbi.com/v1.0/myorg/groups"
</p><p>        $body = "{`"name`":`"myNewGroup`"}"
</p><p>        $response = Invoke-RestMethod -Uri $uri -Headers $auth_header -Method POST -Body $body <span style="color:red">-ContentType 'application/json'</span>
	</p><p>        $target_group_id = $response.id
</p><p>
 </p><p>
 </p><p>
 </p><p>
 </p>