---
title: Cannot load type for DbProviderTypeName MySql.Data.MySqlClient.MySqlClientFactory
description: "Learn why the 'Cannot load type for DbProviderTypeName MySql.Data.MySqlClient.MySqlClientFactory' error is thrown and how to resolve it in the Report Server for .NET."
type: troubleshooting
page_title: The MySql.Data Assembly cannot be loaded in the Report Server for .NET
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

Attempting to create a new data connection to a MySQL database with the [MySQL Data Provider for .NET](https://dev.mysql.com/downloads/connector/net/) is unsuccessful in the Telerik Report Server for .NET and an error message is displayed on the screen.

This happens despite the data provider being successfully found and loaded in the dropdown with the available data providers for connecting.

## Error

`Cannot load type for DbProviderTypeName 'MySql.Data.MySqlClient.MySqlClientFactory'.`

## Cause

The Report Server for .NET adds the data provider to the available data providers dropdown because it is installed on the machine and registered in `machine.config`. However, it encounters a failure when trying to load the `MySql.Data.dll` assembly from the root directory during the database connection step. This failure is due to the assembly's absence in the root directory of the application.

## Solution

The issue can be resolved by manually copying the `MySql.Data.dll` assembly to the root directory of the Report Server for .NET:

1. Ensure the MySql data provider is installed on your machine. If not installed, download and install it from the official [MySQL Connector/NET download page](https://dev.mysql.com/downloads/connector/net/).
2. Locate the `MySql.Data.dll` assembly in the installation directory of the MySql Connector/NET. The path to this directory varies based on the installed version. For example, if you have installed `MySql Connector NET 8.0.31`, the path might be `C:\Program Files (x86)\MySQL\Connector NET 8.0\Assemblies`.
3. Copy the `MySql.Data.dll` assembly from its installation directory to the Report Server for .NET root directory, typically located at `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web.NET`.
4. After copying the assembly, reload the Report Server page and attempt to re-create the data connection.

## See Also

* [MySQL Connector/NET Documentation](https://dev.mysql.com/doc/connector-net/en/)
