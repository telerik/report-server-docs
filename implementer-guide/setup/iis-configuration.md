---
title: IIS Configuration
page_title: IIS Configuration
description: IIS Configuration
slug: iis-configuration
tags: iis
published: true
position: 203
---

# IIS Configuration

The Report Server installer performs a basic setup of the new Report Server web app by adding an HTTP binding under port 83, if available, or under the first subsequent available port. We recommend setting up an HTTPS-secured binding for the production deployment. We also recommend applying additional settings in IIS to compress resources sent from the Report Server to the clients and improve load times:

The first step is to enable static and dynamic HTTP compression for the Report Server website. The Microsoft article [HTTP Compression](https://learn.microsoft.com/en-us/iis/configuration/system.webserver/httpcompression/) provides a detailed guide.

The second step is to allow dynamic HTTP compression to compress application/json responses. This step is recommended when the Web Report Designer is enabled in Report Server and the designer requests large reports from the server. Large reports are considered to be reports containing many report items or embedded resources, such as images or CSV/JSON data.
Allowing this type of compression is done in [ApplicationHost.config](https://docs.microsoft.com/en-us/iis/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig). The location of the file is in the *%windir%\system32\inetsrv\config* directory. Add the following mime type to *httpCompression > dynamicTypes*:

`````
	<httpCompression directory="%TEMP%\iisexpress\IIS Temporary Compressed Files">
		<scheme name="gzip" dll="%IIS_BIN%\gzip.dll" />
		<dynamicTypes>
			...

			<!-- compress JSON responses from Web API -->           
			<add mimeType="application/json" enabled="true" /> 

			...
		</dynamicTypes>
		<staticTypes>
			...
		</staticTypes>
	</httpCompression>
`````

It is recommended to stop IIS before applying changes to the [ApplicationHost.config](https://learn.microsoft.com/en-us/iis/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig).

## Preserving IIS Settings

>note The __Report Server for .NET Framework__ preserves IIS Settings only when installed with the __LocalSystem__ identity which uses elevated permissions. The IIS Settings cannot be preserved for technical reasons with the limited _ReportServerUser_.

The _Telerik Report Server_ settings applied in the IIS console, including the HTTPS bindings and AppPool identity, will be preserved if you are with version [R3 2023 SP1 (9.2.23.1114)](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-r3-2023-sp1-9-2-23-1114) or later and upgrade to a newer version.

When upgrading from _Telerik Report Server_ `9.2.23.1010 or older`, you must reapply the IIS Settings after the upgrade.

This means that if you need to automatically preserve the IIS Settings, first you must upgrade to `9.2.23.1114 or later` and reapply the settings.

__Example__:

* IIS settings will be lost

	When upgrading from `9.0.23.118` to `10.0.24.131`
	
	When upgrading from `9.2.23.1010` to `9.2.23.1114`

* IIS settings will be kept

	When upgrading from `9.2.23.1114` to `10.0.24.131`
	
	When upgrading from `10.0.24.131` to `10.1.24.605`
