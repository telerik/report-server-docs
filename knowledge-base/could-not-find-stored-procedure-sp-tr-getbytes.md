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
The Report Server application fails to start and an error message *'Could not find stored procedure 'sp_tr_GetBytes'* appears.

## Solution
The error could occur if using [MsSqlServerStorage](https://docs.telerik.com/report-server/implementer-guide/setup/storage-settings) which requires an MSSQL database.

Please test the following:
1. On an accessible by the server machine MSSQL Server, create a blank database;
2. Close all browsers;
3. Uninstall and reinstall Telerik Report Server in a custom folder, when you are asked where to place the installation. Our recommendation is to use the MSI file from your [Telerik account](https://www.telerik.com/account/) -> Downloads -> Report Server -> MSI and to run the installer as an administrator of the machine;
4. When you start *http://yourreprotserverhost:83* select to use MsSqlServerStorage and provide the connection string to the database configured in step 1. Verify the database is accessible by the identity of the IIS Application pool associated with the Report Server Web part.

## See Also
- [Telerik Report Server Storage Settings](https://docs.telerik.com/report-server/implementer-guide/setup/storage-settings)
- [MsSqlServerStorage Class Remarks](https://docs.telerik.com/reporting/t-telerik-reporting-cache-mssqlserverstorage#remarks)
