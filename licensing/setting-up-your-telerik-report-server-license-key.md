---
title: Setting Up Telerik Report Server License Key
page_title: "Learn how to set up the Telerik Report Server License Key."
slug: license-key
tags: license, key, telerik, report, server
published: True
previous_url: /licensing, /licensing/license-agreement
position: 1
---

# Setting Up Your Telerik Report Server License Key

Starting with the Q1 2025 release, the Telerik Report Server requires activation using a license key — this applies to both the trial and commercial versions of the product. This article describes how to download or update your personal license key and use it to activate the Telerik Report Server product.

An invalid license results in [error and warning]({%slug license-errors-and-warnings%}) indicators such as watermarks and banners.

## Downloading the License Key

To download a license key for the Telerik Report Server, you must have either a commercial or a trial license. If you do not have a license, sign up for a [free trial](https://www.telerik.com/account/trials) first, and then follow the steps below.

1. Go to the [License Keys](https://www.telerik.com/account/your-licenses/license-keys) page in your Telerik account.

1. Click the **Download License Key** button.

	![Download License Key](images/download-license-key.png)

	Alternatively, use the [Progress Control Panel](https://www.telerik.com/download-trial-file/v2/control-panel) to install the Telerik Report Server. The Progress Control Panel automatically downloads the license key file to your home directory. Use the license key file to [activate the Report Server](#activating-telerik-report-server).

## Activating Telerik Report Server (Q2 2025 Release and Onwards)

To activate Telerik Report Server Q2 2025 and future releases, we recommend using the built-in license management:

1. Open the Report Server Manager web interface and log in with an admin user.
1. Select _Configuration_ from the top-right corner.
1. Inside the _Configration_ page, select the _About_ tab.
1. Look for the _Status_ row under the _License Details_ section and choose:
	* _Add_ if you are setting up a license for the first time
	
	![An image displaying how the About section of the Configuration page looks without a license.](images/configuration-page-about-no-license.png)
	
	* _Edit_ if you are renewing or updating an existing license
	
	![An image displaying how the About section of the Configuration page looks with applied license.](images/configuration-page-about-with-license.png)
	
1. The newly opened license management dialog allows you to add or edit a key by:
	* choosing a file from the filesystem - accepts only _TXT_ files with valid JWT content
	* pasting a key content inside the text area - accepts only valid JWT content
	
	![An image of how the "Add License Key" window looks like when opened.](images/add-license-key-window.png)
	
1. Select where the license key should be stored:
	* Application Root Folder writes the license key to a `telerik-license.txt` file and stores it inside the `C:\Program Files (x86)\Progress\Telerik Report Server\` directory. After submitting the new license, the _Report Server Manager_ activates the new license instantaneously. However, the _Report Server Agent_ service requires a manual restart for the changes to take effect.
	* User's Environment Variables stores the license key in an environment variable tied to the user who runs the Report Server IIS application. License re-validation requires an IIS reset and Report Server Agent restart for the changes to take effect.
1. Select _Submit_ to apply the license key for the Report Server Manager application.
1. Open Windows's **Services** app by selecting `Windows Key` + `R` to open the Run window, and then enter `services.msc`.
10. Scroll to the `Telerik.ReportServer.ServiceAgent` service instance and right-click it -> `Restart`.

	![An image displaying how to restart the Telerik.ReportServer.ServiceAgent process from the Windows Services app.](images/windows-services-restart-service-agent.png)

1. Wait for the `Telerik.ReportServer.ServiceAgent` process to restart.

## Activating Telerik Report Server (Q1 2025 Release)

To activate the Q1 2025 version of Telerik Report Server:

* When deploying the Report Server in a cloud environment, create an Environment Variable named `TELERIK_LICENSE` and add the text content of your Telerik Report Server license key file as a value.

* When deploying the Report Server on your local environment, copy the `telerik-license.txt` license key file to the installation folder of the Telerik Report Server or any parent folder. By default, this is `C:\Program Files (x86)\Progress\Telerik Report Server\`. This step makes the license key available to both the [Report Server Manager]({%slug search%}) and [Report Server Agent]({%slug service-agent%}).

To make the license key available to individual Reporting Engine components, copy the file to the following folder:

* For __Report Server Manager__, the default folder is `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\`.
* For __Report Server Agent__, the default folder is `C:\Program Files (x86)\Progress\Telerik Report Server\Services\`.

When you run Telerik Report Server, it automatically locates the license environment variable or license file and activates the product.

## Updating Your License Key

Whenever you purchase a new license or renew an existing one, always [download](#downloading-the-license-key) and apply a new license key. The new license key includes information about all previous license purchases. This process is referred to as a *license key update*. Once you have the new license key, use it to [activate Telerik Report Server](#activating-telerik-report-server).

# See Also

* [License Activation Errors and Warnings]({%slug license-errors-and-warnings%})
* [Frequently Asked Questions about Your Telerik Report Server License Key]({%slug license-frequently-asked-questions%})
