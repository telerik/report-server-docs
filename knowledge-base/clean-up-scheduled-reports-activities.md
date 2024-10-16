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

When using Telerik Report Server for an extended period, the UI for editing reports can become slow due to the accumulation of activity records. This article outlines methods to clean out old scheduled reports activities to improve performance.

This KB article also answers the following questions:
- How to delete old executions of scheduled tasks in Telerik Report Server?
- What is the SQL script to remove historical activity data in Report Server?
- How to use the Report Server REST API to manage scheduled task documents?

## Solution

### Using the Report Server REST API

1. Use the `GET api/reportserver/v2/scheduledtasks` request to retrieve all scheduled tasks. Refer to the [Report Server REST API documentation](https://docs.telerik.com/report-server/implementer-guide/apis/rest-api/v2/get-api-reportserver-v2-scheduledtasks) for details.
2. Use `GET api/reportserver/v2/executions/scheduledtasks/{scheduledTaskId}` to get all executions for a specific scheduled task. Inspect the `ExecutionDate` property to identify executions to delete.
3. Use `DELETE api/reportserver/v2/executions/scheduledtasks/{scheduledTaskId}/{executionId}` to delete specific executions based on your criteria.

For more information on using the REST API, consult the [Report Server API Client documentation](https://docs.telerik.com/report-server/implementer-guide/apis/rest-api/report-server-api-client).

### Using SQL Script

1. **Backup the database** following the instructions in the [Storage Backup article](https://docs.telerik.com/report-server/implementer-guide/setup/storage-backup).
1. **Delete all scheduled task documents** using the following SQL statement:

```sql
DELETE [ReportServer].[dbo].[tr_Object]
WHERE Id LIKE 'TRS\1\Sd%'
```

Remember to replace `[ReportServer]` with your database name. The scripts aim to delete records related to cached data and scheduled task executions.

## See Also

- [Report Server REST API](https://docs.telerik.com/report-server/implementer-guide/apis/rest-api/v2/api-reference) - Official documentation for Report Server REST API.
- [Storage Backup - Telerik Report Server](https://docs.telerik.com/report-server/implementer-guide/setup/storage-backup) - Guide on creating a backup of the Report Server Storage.
- [Report Server API Client - Telerik Report Server](https://docs.telerik.com/report-server/implementer-guide/apis/rest-api/report-server-api-client) - Documentation on the Report Server API Client.
