---
title: How to configure Telerik Report Server to use reports with custom functions
description: How to configure Telerik Report Server to use reports with custom functions
type: how-to
page_title: How to configure Telerik Report Server to use reports with custom functions
slug: how-to-use-custom-function-in-report-server
tags: programming,functions,aggregates
ticketid: 1148325
res_type: kb
---

## Environment

<table>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server</td>
	</tr>
</table>

## Description

Extending the report engine of the Report Server is not supported out of the box. It requires some manual steps.

## Solution

1. Copy the assembly containing the user function(s) in:

	* The bin folder of the __Report Server web application__, i.e. `[Telerik Report Server installation folder]\Telerik.ReportServer.Web\bin` (usually `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\bin`)
	* for __scheduling services__ only - in the folder of the scheduling service, i.e. `[Telerik Report Server installation folder]\Services` (usually `C:\Program Files (x86)\Progress\Telerik Report Server\Services`)

1. Register the same assembly in the corresponding application configuration files, using the snippets that could be found in the article [Telerik Reporting assemblyReferences Element](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/assemblyreferences-element).

	* for __Report Server web application__:

		1. in versions up to `R3 2018 SP2 (4.2.18.1129)` in `[Telerik Report Server installation folder]\Telerik.ReportServer.Web\Web.config` (usually `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\Web.config`)
		1. from version `R1 2019 (5.0.19.116)` in `[Telerik Report Server installation folder]\Telerik.ReportServer.Web\TelerikReporting.config` (usually `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\TelerikReporting.config`)

	* for __scheduling services__ only:

		1. in versions up to `R3 2018 SP2 (4.2.18.1129)` in `[Telerik Report Server installation folder]\Services\Telerik.ReportServer.ServiceAgent.exe.config` (usually `C:\Program Files (x86)\Progress\Telerik Report Server\Services\Telerik.ReportServer.ServiceAgent.exe.config`)
		1. from version `R1 2019 (5.0.19.116)` in `[Telerik Report Server installation folder]\Services\TelerikReporting.config` (usually `C:\Program Files (x86)\Progress\Telerik Report Server\Services\TelerikReporting.config`)

1. (_optional_) If the custom functions are aggregate functions, it would be necessary for the Telerik Reporting version used for creating the custom assembly, and the one used in the Telerik Report Server to match.
1. (_optional_) If the Telerik Reporting version on the Report Server is different, add a binding redirect to point to the version of Telerik Reporting used to create the custom function in the same way as explained in the article [Standalone Report Designer Configuration File](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/configuration/overview).
