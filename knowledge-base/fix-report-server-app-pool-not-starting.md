---
title: Fixing Report Server App Pool That Won't Start
description: Resolving issues related to the Report Server application pool failing to start due to invalid identity or missing user rights.
type: how-to
page_title: Resolving Report Server Application Pool Not Starting Issue
meta_title: Resolving Report Server Application Pool Not Starting Issue
slug: fix-report-server-app-pool-not-starting
tags: report-server, app-pool, identity, password, user-rights, troubleshoot
res_type: kb
ticketid: 1682185
---

## Environment

<table>
<tbody>
<tr>
<td>Product</td>
<td>Report Server</td>
</tr>
<tr>
<td>Version</td>
<td>10.2.24.924</td>
</tr>
</tbody>
</table>

## Description

I cannot start the Report Server application pool in IIS. Attempting to log in results in a 503 error stating "The Service is unavailable." The Windows log shows that the identity of the application pool is invalid, possibly due to incorrect username/password or missing batch logon rights. Restarting the application pool leads to immediate failure.

This knowledge base article also answers the following questions:
- How to fix the Report Server application pool failing to start?
- Why does the Report Server application pool show invalid identity?
- How to assign proper user rights for the Report Server application pool?

## Solution

To resolve the issue, follow these steps:

1. Verify whether the password for the `ReportServerUser` account has been changed since installation. If yes:
   - Open IIS Manager.
   - Navigate to Application Pools.
   - Select the `TelerikReportServer` application pool.
   - Go to Advanced Settings -> Process Model -> Identity.
   - Re-enter the updated username and password.

2. Ensure that the `ReportServerUser` account has required user rights:
   - Open Local Security Policy (Search for `secpol.msc` in the Start menu).
   - Navigate to Computer Configuration > Windows Settings > Local Policies > User Rights Assignment.
   - Confirm that the `ReportServerUser` or its user group has the following rights:
     - "Log on as a batch job."
     - "Log on as a service."

3. If the issue persists, troubleshoot further by generating logs:
   - Refer to [Troubleshoot Report Server Manager](https://docs.telerik.com/report-server/knowledge-base/troubleshoot-report-server).
   - Follow the instructions to collect the necessary logs.

4. Before making any changes, create a backup for safety:
   - Refer to [Storage Backup - Telerik Report Server](https://docs.telerik.com/report-server/implementer-guide/setup/storage-backup).

## See Also

- [Report Server Release History](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-2024-q3-(10-2-24-924))
- [Troubleshoot Report Server Manager](https://docs.telerik.com/report-server/knowledge-base/troubleshoot-report-server)
- [Storage Backup - Telerik Report Server](https://docs.telerik.com/report-server/implementer-guide/setup/storage-backup)
