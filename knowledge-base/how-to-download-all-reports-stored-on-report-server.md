---
title: Downloading All Reports Stored on Report Server
description: Download all report defintions that are stored on the report server
type: how-to
page_title: How to Download All Reports Stored on Report Server
slug: how-to-download-all-reports-stored-on-report-server
position:
tags:
ticketid: 1514505
res_type: kb
---

## Environment

<table>
	<tbody>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® Report Server</td>
		</tr>
	</tbody>
</table>

## Description

This article explains how to download all report definitions that are stored on the Report Server with the Report Server API.

## Solution

In our [GitHub repository](https://github.com/telerik/reporting-samples/tree/master/Downloading%20All%20Reports%20Stored%20on%20Report%20Server), you can find a Console application that downloads all TRDP/TRDX reports that are stored on the Report Server. Below are the required steps for building the application:

- Add the following references:
  - Telerik.Reporting;
  - Telerik.ReportServer.HttpClient;
  - Telerik.ReportServer.Services.Models.
- Create a setting for the Report Server connection;

```C#
    var settings = new Telerik.ReportServer.HttpClient.Settings()
        {
            BaseAddress = "http://localhost:83/"
        };
```

- Get all categories in the Report Server and for each of them get the reports:

```C#
    using (var rsClient = new ReportServerClient(settings))
            {
                rsClient.Login("username", "password");
                var categories = rsClient.GetCategories();
                foreach (var category in categories)
                {
                    var reportInfos = rsClient.GetReportInfosInCategory(category.Id);
                    foreach (var reportInfo in reportInfos)
                    {
                        var reportId = reportInfo.Id;
                        var reportDefinition = rsClient.GetLatestReportRevision(reportId);
                        SaveReportDefintion(reportDefinition, reportInfo.Name);
                    }
                }
            }
```

- Finally, save the report definitions:

```C#
private static void SaveReportDefintion(Telerik.ReportServer.Services.Models.ReportRevisionContent reportDefinition, string name)
        {
            var extension =reportDefinition;
            string path = "filepath" + name;
            File.WriteAllBytes(path + reportDefinition.Extension, reportDefinition.Content);
        }
```
