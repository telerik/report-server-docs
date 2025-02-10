---
title: FAQs
page_title: "Frequently Asked Questions about Telerik Report Server Licensing."
slug: license-frequently-asked-questions
tags: license, telerik, report, server, faq, questions
published: True
position: 9
---

# Frequently Asked Questions

This article lists the answers to the most frequently asked questions (FAQs) about working with the Telerik Report Server license key.

## Does the license key expire?

Yes, the license key expires at the end of your support subscription:

* For trial users, this is at the end of your 30-day trial.
* For commercial license holders, this is when your subscription term expires.

You will need to obtain and install a new license key after starting a trial, renewing a license, or upgrading a license.

> An expired perpetual license key is valid for all Telerik Report Server versions installed before its expiration date.

## Will the product function with an expired license key?

This depends on your license type.

* __Perpetual licenses__ will continue to function normally with an expired license key. However, the following will happen if you update or install a Report Server version that is released after the expiration date of the license:

	- A watermark appears on each report document page
	- A warning message similar to the one shown below is logged in the trace log after attaching a Trace Listener to the [Report Server Manager]({%slug search%}) and [Report Server Agent]({%slug service-agent%})

* __Subscription licenses__ will prevent you from installing the Report Server application with an expired license key. Deployed instances will continue to function normally.
* __Trial licenses__ will prevent you from running the Report Server. The following will happen if you try to run the application:

	- A watermark appears on each report document page.
	- A warning message similar to the following is logged in the build log after attaching a Trace Listener to the Report Server Manager and Report Server Agent:

````
Telerik and Kendo UI Licensing warning TKL002: No Telerik and Kendo UI License file found.
Telerik and Kendo UI Licensing warning TKL002: The following locations were searched:
Telerik and Kendo UI Licensing warning TKL002:  * TELERIK_LICENSE (EnvironmentVariable)
Telerik and Kendo UI Licensing warning TKL002:  * KENDO_UI_LICENSE (EnvironmentVariable)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\telerik-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\kendo-ui-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\Progress\Telerik Report Server\Services\telerik-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\Progress\Telerik Report Server\Services\kendo-ui-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\Progress\Telerik Report Server\telerik-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\Progress\Telerik Report Server\kendo-ui-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\Progress\telerik-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\Progress\kendo-ui-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\telerik-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Program Files (x86)\kendo-ui-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\telerik-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\kendo-ui-license.txt (RecursiveFilePath)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Users\user1\AppData\Roaming\Telerik\telerik-license.txt (UserDirectory)
Telerik and Kendo UI Licensing warning TKL002:  * C:\Users\user1\AppData\Roaming\Telerik\kendo-ui-license.txt (UserDirectory)
Telerik and Kendo UI Licensing warning TKL002: Activate a License Key file at https://prgress.co/3PBSVoC
Telerik and Kendo UI Licensing warning TKL101: Telerik Reporting is not listed in your current license file.
Telerik and Kendo UI Licensing warning TKL004: Unable to locate licenses for all products.
````

See the [Invalid License]({%slug license-errors-and-warnings%}#invalid-license) section for more information.

Note that future updates of Telerik Report Server may restrict or disable some features when no valid license is present.

## I updated the Telerik Report Server and the invalid license errors have appeared. What is the cause of this behavior?

If this happens, the possible reason is that the end date of the license activated in your application is before the release date of the newly installed product. To fix this issue:

1. [Download a new license key]({%slug license-key%}#downloading-the-license-key).
1. [Activate the new license key]({%slug license-key%}#activating-telerik-reporting) in your project.

## Do I need an Internet connection to activate the license?

No, the license activation and validation are performed entirely offline.

The license is not validated with our services at any point in the project lifecycle.

## What happens if both the environment variable and the license key file are present?

If both the `TELERIK_LICENSE` environment variable and the `telerik-license.txt` file are present, then the environment variable will be used.

To enforce the use of the license key file, unset the environment variable.

## Are earlier versions of Telerik Report Server affected?

No, versions released before __January 2025__ do not require a license key.

# See Also

* [License Activation Errors and Warnings]({%slug license-errors-and-warnings%})
* [Setting Up Your License Key]({%slug license-key%}))
* [License Agreement](https://www.telerik.com/purchase/license-agreement/report-server)
* [Troubleshooting Report Server]({%slug troubleshoot-report-server%})
* [Troubleshooting Report Server for .NET]({%slug troubleshoot-report-server-net%})
