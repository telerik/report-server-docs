---
title: Errors and Warnings
page_title: "Learn about Errors and Warnings in Telerik Report Server Licensing."
slug: license-errors-and-warnings
tags: license, telerik, report, server, questions, errors, warnings
published: True
position: 7
---

# License Activation Errors and Warnings

Starting with the 2025 Q1 release, using the Telerik Report Server without a license or with an invalid license causes specific license warnings and errors. This article defines what an invalid license is, explains what is causing it, and describes the related license warnings and errors.

If a valid license cannot be found:

- A watermark appears on each document page in the report.
- A [warning message](#license-warnings-and-errors) appears in the log file generated after attaching a Trace Listener to the [Report Server Manager]({%slug search%}) and [Report Server Agent]({%slug service-agent%}):

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

## Invalid License

An invalid license can be caused by any of the following:

* Using an expired subscription license. Subscription licenses expire at the end of the subscription term.
* Using a perpetual license for Telerik Report Server versions released outside the validity period of your license.
* Using an expired trial license.
* A missing license for the Telerik Report Server.
* Not installing a license key in your application.
* Not updating the license key after renewing your Telerik Report Server license.

## License Warnings and Errors

Using the Telerik Report Server with an expired or missing license, the `Telerik.Licensing` will indicate the following errors or conditions:

|Condition or Error|Message Code|Solution|
|----|----|----|
|`No Telerik and Kendo UI License file found`|TKL002|[Set up a license key]({%slug license-key%}) to activate Telerik Report Server and remove the error message.|
|`Corrupted Telerik and Kendo UI License Key content`|TKL003|[Download a new license key]({%slug license-key%}#downloading-the-license-key) and use it to activate Telerik Report Server and remove the error message.|
| `Unable to locate licenses for all products` | TKL004 | Your license is not valid for all Telerik and Kendo products added to your project. If you have already purchased the required license, then [update your license key]({%slug license-key%}). |
|`Your subscription has expired`|TKL103; TKL104|Renew your subscription and [download a new license key]({%slug license-key%}#downloading-the-license-key).|
|`Your current license has expired`|TKL102|You are using a product version released outside the validity period of your perpetual license. To remove the error message, do either of the following: <ul><li>Renew your subscription and [download a new license key]({%slug license-key%}#downloading-the-license-key)</li><li>Downgrade to a Telerik Report Server version covered by your perpetual license, as specified in the message.</li></ul>|
|`Your trial expired`|TKL105|Purchase a commercial license to continue using the product.|
|`Telerik Reporting is not listed in your current license file`|TKL101|Review the purchase options for the listed products.|
| `No Telerik or Kendo UI product references detected in project.` | TKL001 | If you use Telerik products and see this message, update the `Telerik.Licensing` package to version `1.4.9` or later. If you do not use Telerik products, remove the `Telerik.Licensing` NuGet reference from your project |

# See Also

* [Setting Up Your License Key]({%slug license-key%})
* [Frequently Asked Questions about Your Telerik Report Server License Key]({%slug license-frequently-asked-questions%})
* [License Agreement](https://www.telerik.com/purchase/license-agreement/report-server)
* [Troubleshooting Report Server]({%slug troubleshoot-report-server%})
* [Troubleshooting Report Server for .NET]({%slug troubleshoot-report-server-net%})
