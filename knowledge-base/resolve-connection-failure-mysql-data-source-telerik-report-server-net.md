---
title: Resolving Connection Failure with MySql.Data Source in Telerik Report Server
description: A guide on fixing a connection failure issue when connecting to a MySql.Data source in Telerik Report Server due to a missing assembly.
type: troubleshooting
page_title: How to Fix Connection Failure with MySql.Data Source in Telerik Report Server
slug: resolve-connection-failure-mysql-data-source-telerik-report-server-net
tags: report server, mysql.data, connection failure, troubleshooting
res_type: kb
ticketid: 1659384
---

## Environment

| Product | Progress® Telerik® Report Server |
| --- | --- |
| Version | 10.1.24.709 |

## Description

Attempting to connect to a MySql.Data source results in a connection failure with the error message: "Cannot load type for DbProviderTypeName 'MySql.Data.MySqlClient.MySqlClientFactory'." This issue occurs after a fresh installation of the .NET version of Report Server and is due to the inability to connect because the MySql.Data.dll assembly is not present in the root directory.

## Cause

The Report Server can locate the installed MySql data provider. However, it encounters a failure when trying to load the `MySql.Data.dll` assembly from the root directory during the database connection step. This failure is due to the assembly's absence in the specified directory.

## Solution

To resolve this issue, manually copy the `MySql.Data.dll` assembly to the root directory of the Report Server. Follow these steps:

1. Ensure the MySql data provider is installed on your machine. If not installed, download and install it from the official [MySQL Connector/NET download page](https://dev.mysql.com/downloads/connector/net/).
2. Locate the `MySql.Data.dll` assembly in the installation directory of the MySql Connector/NET. The path to this directory varies based on the installed version. For example, if you have installed MySql Connector NET 8.0.31, the path might be `C:\Program Files (x86)\MySQL\Connector NET 8.0\Assemblies`.
3. Copy the `MySql.Data.dll` assembly from its installation directory to the Report Server root directory, typically located at `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web.NET`.
4. After copying the assembly, reload the Report Server page and attempt to re-create the MySql.Data source connection.

## See Also

- [Telerik Report Server Documentation](https://docs.telerik.com/report-server/)
- [MySQL Connector/NET Documentation](https://dev.mysql.com/doc/connector-net/en/)
