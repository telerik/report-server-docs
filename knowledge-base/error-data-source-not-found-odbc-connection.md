---
title: Error Data source name not found
description: Error Data source name not found and no default driver specified
type: troubleshooting
page_title: Error Data source name not found
slug: error-data-source-not-found-odbc-connection
tags: odbc
res_type: kb
---

## Environment

<table>
 <tr>
  <td>Product</td>
  <td>Progress® Telerik® Report Server</td>
 </tr>
 <tr>
  <td>Operating System</td>
  <td>Windows</td>
 </tr>
</table>


## Description

The message 'Data source name not found and no default driver specified' appears when Standalone Report Designer tries to open an ODBC connection, registered in Telerik Report Server, although the connection string is valid and ODBC DSN is registered as User DSN.

## Solution

When a DSN is registered as [User DSN](https://support.microsoft.com/en-us/help/966915/user-dsn-vs-system-dsn), this means that only the currently logged-in user can access it. The Report Server pool uses [LocalSystem](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/31d57870-1faa-4e14-8527-ce77b1ff40e4/local-service-local-system-or-network-service?forum=sqlsecurity) built-in account by default, so it probably is unable to access the registered User DSN. The solution is to register the DSN as System DSN in ODBC Data Source Administrator, so it will be available to all users.
