---
title: Setting Up Telerik Repor Server License Key
page_title: "Learn how to set up the Telerik Report Server License Key."
slug: license-key
tags: license, key, telerik, report, server
published: True
previous_url: /licensing
position: 1
---

# Setting Up Your Telerik Report Server License Key

Starting with the Q1 2025 release, the Telerik Report Server requires activation through a license key (trial or commercial). This article describes how to download or update your personal license key and use it to activate the Telerik Report Server product.

An invalid license results in [errors and warnings]({%slug license-errors-and-warnings%}) during build and run-time indicators such as watermarks and banners.

The implementation of the 2025 licensing requirements will occur in two phases:

- Phase 1 - Starting with the 2025 Q1 release, a missing or invalid license for the trial distributions causes [trial message watermark in the reports]({%slug license-errors-and-warnings%}). The commercial distributions of the product do not exhibit any functional restrictions.
- Phase 2 - Starting with the 2025 Q2 release, there will be only one distribution of the product with different licenses. A missing or invalid license will result in [run-time indicators]({%slug license-errors-and-warnings%}), such as watermarks.

Note that future updates of the product may restrict or disable some features when no valid license is present. You can send us feedback through the _Contact Us_ form or by [opening a support ticket](https://www.telerik.com/account/support-center/contact-us?utm_source=licensing&utm_medium=console&utm_campaign=no_references).

## Downloading the License Key

To download a license key for the Telerik Report Server, you must have either a developer license or a trial license. If you are new, you can sign up for a [free trial](https://www.telerik.com/account/trials) first, and then follow the steps below.

1. Go to the [License Keys](https://www.telerik.com/account/your-licenses/license-keys) page in your Telerik account.
1. Click the **Download License Key** button.

	![Download License Key](images/download-license-key.png)

	The [Progress Control Panel](https://www.telerik.com/download-trial-file/v2/control-panel), and the automated MSI installer of Telerik Report Server will automatically download and store your license key in your home directory. You may use this file to [activate the Report Server](#activating-telerik-report-server).

## Activating Telerik Report Server

To activate the Telerik Report Server:

* When deploying the Report Server on a cloud environment, you may create an Environment Variable named `TELERIK_LICENSE` and add your Telerik Report Server license key as a value.
* On a local environment, copy the `telerik-license.txt` license key file to the installation folder of the Telerik Report Server, by default, `C:\Program Files (x86)\Progress\Telerik Report Server\` or any parent folder. This makes the license key available to both the [Report Server Manager]({%slug search%}) and [Report Server Agent]({%slug service-agent%}).

	You may also copy the license key file to the following subfolders, making it available for the corresponding Reporting Engine:
	
	* for __Report Server Manager__, the default folder is `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\`
	* for __Report Server Agent__, the default folder is `C:\Program Files (x86)\Progress\Telerik Report Server\Services\`;

When you run Telerik Report Server, it automatically locates the license environment variable or license file and activates itself.

## Updating Your License Key

Whenever you purchase a new license or renew an existing one, always [download](#downloading-the-license-key) and install a new license key. The new license key includes information about all previous license purchases. This process is referred to as a license key update. Once you have the new license key, use it to [activate Telerik Report Server](#activating-telerik-report-server).

# See Also

* [License Activation Errors and Warnings]({%slug license-errors-and-warnings%})
* [Frequently Asked Questions about Your Telerik Report Server License Key]({%slug license-frequently-asked-questions%})
