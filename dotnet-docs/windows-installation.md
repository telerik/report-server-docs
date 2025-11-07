---
title: Installation on Windows
page_title: Installing Report Server for .NET on Windows
description: "Learn how to install Telerik Report Server for .NET on Windows using the dedicated MSI installer, including prerequisites, step-by-step installation, and troubleshooting."
slug: dotnet-installation-on-windows
tags: installation,dotnet,windows
published: True
position: 2
---

# Report Server for .NET: Installation on Windows

Starting with 2025 Q4, a dedicated Report Server for .NET (RS.NET) installer is available. This article explains how to install RS.NET on Windows and covers the available installation scenarios.

> Prior to 2025 Q4, RS.NET was distributed with the [.NET Framework 4.6.2 installer]({%slug installation%}). If you use an older version that features this combined installer, make sure to click **Customize** during installation to include RS.NET.

## Prerequisites

Before installing RS.NET, ensure that:

- [System Requirements]({%slug system-requirements%})
- [ASP.NET Core Hosting Bundle](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/?view=aspnetcore-8.0) for IIS deployment

> The installation wizard displays a warning if the ASP.NET Core Hosting Bundle is not available. Ignoring it is not recommended, as this makes the installed Report Server non-functional.

## Downloading the Installer

To download the RS.NET installer:

1. Navigate to [Downloads | Your Account](https://www.telerik.com/account/downloads).
1. Click **Progress® Telerik® Report Server**.
1. Select the desired version from the dropdown menu, then locate `Telerik_ReportServer_NET_{Your Version}.msi` and click on it to download the installer.

## Installing Report Server for .NET

To install RS.NET for the first time:

1. Double-click the downloaded MSI file to start the installer.
1. Read the license agreement and click **I Agree - Continue**.
1. Optionally, choose **Customize** to customize the installed options, then click **Next**.
    >caution The RS.NET installer currently does not currently include SDK examples. This may be added in future releases.
1. Choose a user option and click **Next**. Creating a dedicated Windows user (`RSUserNET`) is recommended for security purposes. For more information about the available user options, see [ReportServerUser, LocalSystem Identity and Dedicated Users]({%slug installation%}#reportserveruser-localsystem-identity-and-dedicated-users).
1. Click **Install** to proceed with the installation.

The installer automatically creates IIS applications on port 81 (RS.NET) and port 82 (RS.NET Service Agent). If these ports are unavailable, it assigns the next available ones.

When you first access RS.NET, you will be prompted to configure storage and register an administrator user.

## Upgrading Report Server for .NET

To upgrade RS.NET from a previous version, run the new installer MSI file and follow the same installation steps mentioned in the [Installing Report Server for .NET](#installing-report-server-for-net) section.

When upgrading from the combined MSI installer (versions prior to 2025 Q4), environment variables (such as encryption keys) are automatically migrated to the newly selected user option (for example, `RSUserNET` if creating a dedicated Windows user).

>caution The RS.NET installer does not support automatic backup. Make sure to perform a [manual storage backup]({%slug storage-backup%}#manual-backup) before upgrading to avoid data loss.

## Troubleshooting

If scheduled tasks, data alerts, or email functionality is not working, the [Report Server Agent]({%slug service-agent%}) connection may not have configured automatically. See [Manual Configuration of RS.NET Service Agent Connection]({%slug manual-configuration-rs-net-service-agent%}) for detailed steps on how to do this manually.

For issues like missing or corrupt files, use the installer's repair functionality:

1. Run the same MSI installer again and click **Next**.
2. Select **Repair** to start the process.