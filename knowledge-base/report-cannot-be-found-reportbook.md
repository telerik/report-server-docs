---
title: Report cannot be found error when previewing report book in Report Server
description: When previewing report book in Report Server an error Report cannot be found is shown
type: troubleshooting
page_title: ReportBook shows Report cannot be found error
slug: report-cannot-be-found-reportbook
position:
tags: reportbook
ticketid: 1159773
res_type: kb
---

## Environment

<table>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server (with 15 CAL users)</td>
	</tr>
</table>

## Description

Previewing report book in Telerik Report Server results in an error.

## Error Message

```
Unable to get report parameters.
An error has occurred.
'ReportName.trdp' report cannot be found.
```

## Cause\Possible Cause(s)

A possible cause is that report book was created locally but not on the Report Server. When creating a new report or report book in Standalone report designer, there are two options where to save it: locally or on the Report Server.

When report book is saved locally, reports added to the report book would be referenced using relative paths to those reports. When report book is saved on the server reports would be referenced using their location on the server, for example: **[CategoryName]/[ReportName]**. In this case, report will be referenced only by its name without file extension.

After report book that was created localy is uploaded to Report Server and previewed in the viewer, the above-mentioned error is shown because the path to the local report file cannot be resolved.

## Solution

To correct the path to the reports, follow these steps:

1. Open the report book in Standalone designer using **File menu | Open | Report Servers**
1. Delete existing reports and select new ones that are stored on the server

## See Also

- [Working with Report Server Reports](https://docs.telerik.com/reporting/standalone-report-designer-working-with-server-reports#reference-another-report-stored-in-the-server)
