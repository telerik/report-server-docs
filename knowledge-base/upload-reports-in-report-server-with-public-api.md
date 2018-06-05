---
title: Add reports to Report Server programmatically
description: Upload reports to Report Server from the code
type: how-to
page_title: Use Report Server API to upload reports 
slug: upload-reports-in-report-server-with-public-api
position: 
tags: 
ticketid: 1168719
res_type: kb
---

## Environment
<table>
	<tr>
		<td>Product Version</td>
		<td>4.1 18.516</td>
	</tr>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server (with 15 CAL users)</td>
	</tr>
</table>


## Description
How to upload a report in the Report Server using the public API

## Solution
A simple console application in **C#** demonstrating how to upload a report (_Concentric_NumericalScale_test.trdx_ that is included in the project) programmatically using the Report Server API is available in the attached [UseReportServerApi.zip file](https://www.telerik.com/docs/default-source/knowledgebasearticleattachments/reporting/usereportserverapi.zip?sfvrsn=7c04b2b5_2).

It is necessary to change the Log-in details to reflect your local settings, i.e. modify the following code accordingly:
```CSharp
class Program
{
    static void Main(string[] args)
    {
        ReportServerClient reportServerClient = new ReportServerClient(@"http://arabadzhiev:83/api/reportserver/");// Change 'arabadzhiev:83' to 'the local report server host:port'
        reportServerClient.Login("arabadzhiev", "arabadzhiev");// Specify the real 'UserName' and 'Password' in this order

        .....
    }
}
```
