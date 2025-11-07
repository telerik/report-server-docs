---
title: Manual Configuration of RS.NET Service Agent Connection
description: "Learn how to manually configure the connection between Report Server for .NET and its Service Agent when automatic configuration fails."
type: troubleshooting
page_title: Manual Configuration of RS.NET Service Agent Connection
slug: manual-configuration-rs-net-service-agent
tags: rs.net,service-agent,configuration,troubleshooting,installation
res_type: kb
---

## Environment

<table>
	<tbody>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® Report Server</td>
		</tr>
		<tr>
			<td>Product Version</td>
			<td>2025 Q4</td>
		</tr>
	</tbody>
</table>

## Description

During RS.NET installation, the installer automatically configures the connection between the RS.NET web application and the RS.NET Service Agent. However, if the automatic configuration fails, you may need to [manually configure this connection](#solution). In case the automatic configuration fails, opening `http://localhost:82/api/system/isalive` in the browser returns `404`.

> For versions prior to 2025 Q4 that relied on a combined installer for both RS and RS.NET, the RS.NET Service Agent is likely hosted on port 84 instead, and the URL should be `http://localhost:84/api/system/isalive`.

The automatic RS.NET configuration and initialization process involves the following steps: 

1. When RS.NET starts for the first time, you go through the **Configure Storage** and **Register Administrator** pages. As a result, the settings are stored in the `ReportServerAdmin.json` file.
1. RS.NET checks its `appsettings.json` configuration file for the `InitialAgentUrl` key. This should contain a valid URL like `http://localhost:82` where the Service Agent is registered.
1. RS.NET calls the Service Agent URL and passes storage settings to it. These are saved in `ServiceAgent.json` in the Service Agent's directory.

## Solution

If the automatic configuration fails, follow these steps:

1. Delete the file `{Installation Folder}\Telerik Report Server .NET\Services\ServiceAgent.json` from RS.NET Service Agent's folder if it exists.
1. Test whether the RS.NET Service Agent responds by calling the RS.NET Service Agent endpoint `/api/system/isalive` from the browser. By default, this is the URL `http://localhost:82/api/system/isalive`.
1. Open RS.NET's `appsettings.json` configuration file and add/edit the key `"InitialAgentUrl": "http://localhost:82"`. The value in the example assumes the RS.NET Service Agent is running on port _82_. Change the URL based on your settings.
1. Restart the RS.NET and RS.NET Service Agent.
1. Check the RS.NET's **Configuration** -> **ServiceAgent** page. The entry `"DefaultServiceAgent" : "http://localhost:82"` should now be present. The URL may differ, depending on your settings.
1. To use the RS.NET Service Agent, ensure the **Mail Server** settings in **Configuration** page are valid.

## See Also

* [Report Server for .NET Installation on Windows]({%slug dotnet-installation-on-windows%})
* [Troubleshooting Report Server for .NET]({%slug troubleshoot-report-server-net%})