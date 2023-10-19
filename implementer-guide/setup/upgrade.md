---
title: Upgrading Report Server
page_title: Upgrading Report Server
description: Upgrading Report Server
slug: upgrade
tags: upgrade
published: true
position: 205
---

# Upgrading Report Server

To upgrade an existing Report Server installation, run a newer version of the [Telerik Report Server Installer]({%slug installation%}) than the installed one.
Telerik Report Server installer replaces all files in the selected installation folder deployed by the previous installer, including the configuration files _/Telerik.ReportServer.Web/Web.config_ and _/Services/Telerik.ReportServer.ServiceAgent.exe.config_.
The only configuration files in the installation folder that will be preserved after the upgrade are _/Telerik.ReportServer.Web/ReportServerAdmin.config_, _/Telerik.ReportServer.Web/TelerikReporting.config_, and _/Services/ServiceAgent.config_.
This way the previously configured assets storage will be preserved after the upgrade as well as any report generation engine configuration options applied in the _/Telerik.ReportServer.Web/TelerikReporting.config_ file.

The installer has a step that [backs up the assets' storage]({%slug storage-backup%}) used from the Report Server. This step is optional and turned on by default. We recommend not skipping it. On the first run after the upgrade, the Report Server will upgrade the assets storage schema version if necessary. Keep the backed-up assets' storage at least until the Report Server is up and running again.

# Before upgrading the Report Server

We advise performing a file backup before upgrading. This is specifically recommended if you have changed the application configuration files _/Telerik.ReportServer.Web/Web.config_ and _/Services/Telerik.ReportServer.ServiceAgent.exe.config_

Note the _Telerik Report Server_ settings applied in the IIS console, including the Bindings. You will need to reapply these after the upgrade. 

# After upgrading the Report Server

After the upgrade progress has passed, open the Report Server Manager (the Finish button of the installer UI will do that by default). This will intrinsically trigger the upgrade of the assets storage schema version if necessary. When the manager loads the default Reports view of the Manager, this upgrade process has passed successfully.

Open the IIS manager and reapply the web application settings, including the Bindings, noted before the upgrade. Make sure the Telerik Report Server web application is working again.

The Report Server Manager is a web application and it is possible to have its styles and scripts cached by the browser, which may result in unpredictable behavior when upgrading or installing a new version. We recommend clearing the browser cache or force-reloading the page, usually with **Ctrl+F5**.
