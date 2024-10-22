---
title: Cleaning Up Scheduled Reports Activities
description: "Learn how to improve performance by deleting old scheduled reports activities in Telerik Report Server using REST API or SQL script."
type: how-to
page_title: How to Delete Old Scheduled Reports Activities
slug: clean-up-scheduled-reports-activities
tags: report server, rest api, scheduled tasks, sql script, performance
res_type: kb
ticketid: 1662255
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

When using Telerik Report Server for an extended period, the UI for editing reports can become slow due to the accumulation of activity records. This article outlines methods to clean out old scheduled report activities to improve performance.

## Solution

### Using the Report Server REST API

1. Use the [GET api/reportserver/v2/scheduledtasks](/implementer-guide/apis/rest-api/v2/get-api-reportserver-v2-scheduledtasks) endpoint to retrieve all scheduled tasks.
1. Use the [GET api/reportserver/v2/executions/scheduledtasks/{scheduledTaskId}](/implementer-guide/apis/rest-api/v2/get-api-reportserver-v2-scheduledtasks-scheduledtaskid) to get all executions for a specific scheduled task. Inspect the `ExecutionDate` property to identify executions to delete.
1. Use the [DELETE api/reportserver/v2/executions/scheduledtasks/{scheduledTaskId}/{executionId}](/implementer-guide/apis/rest-api/v2/delete-api-reportserver-v2-scheduledtasks-scheduledtaskid) endpoint to delete specific executions based on your criteria.

For more information on using the REST API, consult the [Report Server API Client documentation](https://docs.telerik.com/report-server/implementer-guide/apis/rest-api/report-server-api-client).

### MSSQL Storage - Using SQL Script

If the Report Server uses [Microsoft SQL Server (MsSqlServer)]({%slug storage-settings%}#microsoft-sql-server-mssqlserver) storage, the scheduled task executions can be deleted through SQL.

1. **Backup** the database - [Storage Backup]({%slug storage-backup%}).
1. Delete **all** scheduled task documents using the following SQL statement:

````SQL
DELETE [ReportServer].[dbo].[tr_Object]
WHERE Id LIKE 'TRS\1\Sd%'
````

> Replace `[ReportServer]` with the name of the database.

## See Also

* [Report Server API Client - Telerik Report Server]({%slug report-server-api-client%})
* [Report Server REST API](/implementer-guide/apis/rest-api/v2/api-reference)
* [Storage Backup - Telerik Report Server]({%slug storage-backup%})
