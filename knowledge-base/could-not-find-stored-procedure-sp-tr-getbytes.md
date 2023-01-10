---
title: Could not find stored procedure 'sp_tr_GetBytes'
description: After upgrade an error "Could not find stored procedure 'sp_tr_GetBytes'" occurs
type: troubleshooting
page_title: Could not find stored procedure 'sp_tr_GetBytes'
slug: could-not-find-stored-procedure-sp-tr-getbytes
position: 
tags: StorageSettings
ticketid: 1347772
res_type: kb
---

## Environment

<table>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server (with 15 CAL users)</td>
	</tr>
	<tr>
		<td>Operating System</td>
		<td>Windows</td>
	</tr>
</table>

## Description

The Report Server web management application fails with the error message `'Could not find stored procedure 'sp_tr_GetBytes'`.

## Solution

The error could occur when using [MsSqlServerStorage]({%slug storage-settings%}) as it requires a configured MSSQL database.

Please test the following:

1. Create a blank database on an MSSQL server instance accessible by the deployment machine;

2. Close all browsers;

3. Rename or delete the configuration file *{Report Server Installation Folder}\Telerik.ReportServer.Web\ReportServerAdmin.config*

4. When you start `http://yourreportserverhost:83`, select `MsSqlServerStorage` from the initially provided options and enter the connection string to the database configured in step 1. Verify the database is accessible by the identity of the IIS Application pool associated with the Report Server Web part.

If this does not help, try to uninstall and then reinstall Telerik Report Server in a custom folder (configured in the installer). Our recommendation is to use the MSI file from your [`Telerik account`](https://www.telerik.com/account/) -> `Downloads` -> `Progress® Telerik® Report Server` -> MSI and to run the installer with administrator rights. Then execute step 4. again.

## See Also

* [Telerik Report Server Storage Settings]({%slug storage-settings%})
* [MsSqlServerStorage Class Remarks](https://docs.telerik.com/reporting/api/telerik.reporting.cache.mssqlserverstorage#remarks)