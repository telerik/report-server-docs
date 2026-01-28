---
title: How to restrict export formats in Report Preview
description: How to limit the rendering extensions in the Report Preview mode of the Report Server
type: how-to
page_title: How to restrict export formats
slug: how-to-restrict-export-formats-in-preview
position:
tags:
ticketid: 1408256
res_type: kb
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

The article explains how to hide some of the rendering extensions in the Report Preview mode of the Report Server.

## Solution

By default, all rendering extensions in the export options of the viewer of the Report Server are visible.

To hide some of them it will be necessary to set accordingly the [extensions Element](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/extensions-element) of the [Telerik Reporting Configuration]({%slug configure-the-report-engine%}) section of the `TelerikReporting.config` file in the `_Telerik Report Server installation folder_\Telerik.ReportServer.Web`, by default `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web`.

After modifications the config file should look like this:

```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
	<configSections>
		<section name="Telerik.Reporting" type="Telerik.Reporting.Configuration.ReportingConfigurationSection, Telerik.Reporting" allowLocation="true" allowDefinition="Everywhere" />
	</configSections>
	<Telerik.Reporting>
		<extensions>
			<render>
				<extension name="PDF" visible="false">
				</extension>

				<!-- include here all extensions that should be hidden -->

			</render>
		</extensions>
	</Telerik.Reporting>
</configuration>
```

It will be necessary to restart the Report Server after modifying the config so that the changes to take effect.

## See Also

- [Limit export options in ReportViewer to certain format only](https://docs.telerik.com/reporting/knowledge-base/limit-export-options-in-report-viewer)
