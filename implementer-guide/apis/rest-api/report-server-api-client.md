---
title: Report Server API Client
page_title: Report Server API Client
description: Report Server API Client for .NET
slug: report-server-api-client
tags: rest, api, client, net
published: True
position: 10109
---

# Report Server API Client

The Report Server API client is a .NET library which comes in handy when developing .NET applications which would connect to the [Report Server API](slug:rs-v2-api-reference).

The client provides access to the available API endpoints. To gain access to the client and its methods it is required to add the following assembly references:

- `Telerik.ReportServer.HttpClient.dll`
- `Telerik.ReportServer.Services.Models.dll`

The client depends on the following NuGet packages which also have to be added:

- [Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client)
- [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json)

The required assemblies can be found in the Report Server installation folder under **\Tools**. The folder also contains XML files with corresponding names which provide IntelliSense support for Visual Studio.

How to use the client to interact with the Report Server is demonstrated in [Report Server API Client Examples](slug:report-server-api-client-examples).

The client's API reference can be found in [Telerik.ReportServer.HttpClient](https://docs.telerik.com/reporting/n-telerik-reportserver-httpclient).
