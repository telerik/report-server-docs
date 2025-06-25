---
title: Missing Icons and Assets, with Script Errors
description: How to troubleshoot missing icons and assets, with script errors.
type: troubleshooting
page_title: Missing Icons, Assets, or Script Errors
slug: missing-icons-logo-with-script-errors
tags: icons, iis, settings, http, features 
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
			<td>11.1.25.521</td>
		</tr>
	</tbody>
</table>

## Description

Report Server unexpectedly stops showing icons, throws script errors, or has lost whitelabeling features.

![An image demonstrating how the Report Server icons are missing when static content is not enabled](./images/missing-icons-and-logo.png)

Other symptoms may include script errors in the browser console, such as:

- `Uncaught Type Error: Cannot read properties of undefind (reading 'getLocalizatoinString')`
- `Failed to decode downloaded font: host/Contentfonts/TelerikReportServerFont.ttf`

You may also see 404 errors for script and asset links in the Networking tab of the browser **DevTools window**.

## Possible Cause

If the server's IIS setting were reset, either through a Windows Update or other OS operations, that stop allowing access to static content inside the application folder. Some of those assets are image files and JavaScript resources, which results in client-side issues as described above.

## Solution

Re-enable IIS and reselect all relevant features, especially `Internet Information Services` > `World Wide Web Features` > `Common HTTP Features` > `Static Content`. Use the following screenshot for guidance:

![An image demonstrating how to enable static content to be served over HTTP in IIS](./images/iis-settings.png)

> After fixing the IIS settings, if your white labeling customizations are still missing, *disable* the [Whitelabeling]({%slug whitelabeling%}), then reenable it (and reapply customizations).

## See Also

* [IIS Configuration]({%slug iis-configuration%})
* [Whitelabeling]({%slug whitelabeling%})
