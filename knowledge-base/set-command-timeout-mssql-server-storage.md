---
title: How to Set CommandTimeout for the Report Server MSSQL Storage
description: How to set manually CommandTimeout for the Report Server MSSQL Storage
type: how-to
page_title: CommandTimeout for the Report Server MSSQL Storage
slug: set-command-timeout-mssql-server-storage
position:
tags:
ticketid: 1519009
res_type: kb
---

## Environment

<table>
	<tbody>
		<tr>
			<td>Product Version</td>
			<td>7.2.21.1125+</td>
		</tr>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® Report Server</td>
		</tr>
	</tbody>
</table>

## Description

Starting with version [R3 2021 SP2 (7.2.21.1125)](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-r3-2021-sp2-7-2-21-1125), the `CommandTimeout` of the Report Server MSSQL Storage is configurable.

Generally, this should be set when you configure the MSSQL storage from the Configuration page of the Report Server along with the connection string. This is a bug in the Report Server UI that is reported in
[The MSSQL Storage Configuration page doesn't allow setting the CommandTimeout property](https://feedback.telerik.com/report-server/1548474-the-mssql-storage-configuration-page-doesn-t-allow-setting-the-commandtimeout-property).

## Solution

You may configure the value of the `CommandTimeout` property for the MSSQL Storage in the `ReportServerAdmin.config` configuration file of your Report Server web application.

The file resides by default in the installation folder of the Report Server web application, for example,
`C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web`.

Here is a sample code for the config file:

```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="reportServer" type="Telerik.ReportServer.Web.Configuration.ReportServerConfigurationSection, Telerik.ReportServer.Web" requirePermission="false" allowLocation="true" />
  </configSections>
  <reportServer>
    <storage provider="MsSqlServer">
      <parameters>
                <parameter name="ConnectionString" value="Data Source=(local)\MSSQLSERVER01;Initial Catalog=RESTStorage;Integrated Security=SSPI" />
		<parameter name="commandTimeout" value="360" />
      </parameters>
    </storage>
  </reportServer>
</configuration>
```

Edit the file manually to add the command timeout configuration.
