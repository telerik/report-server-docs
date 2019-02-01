---
title: Application Startup
page_title: Application Startup
description: Application Startup
slug: application-startup
tags: project,startup
published: True
position: 300
---

# Application Startup
When you start the report server admin app, it detects if you have already configured it. It requires a set of settings to enable the supported assets management. If these settings are not available, the app starts a two-page setup process for the user.  The user that installed the product usually performs this initial setup. The pages are:

## Step 1/2: Setup storage
The Report Server persists all assets such as reports, scheduled tasks, and users. The supported storage types are File storage, MS SQL Server storage, and Redis storage.

![Setup Storage](../../images/report-server-images/setup_storage_960.png)
By default, the setup page offers the File storage which stores all assets  as files in a target folder. It is the default option as it does not need the installation of extra tools. This makes it perfect for test deployment. This storage suits a production deployment only  if the Report Server instance will not get heavily utilized . For other cases, including multi-instance setup, one of the other options is a must. You can find more info on each supported storage in the [Storage]({%slug storage-settings%}) article. 

The storage settings go into the Report Server configuration file called *ReportServerAdmin.config*. The Report Server installer preserves that file upon upgrade. That way the setting will remain when you upgrade the Report Server version.

## Step 2/2: Register administrator
Once you have setup the target storage, the app can use it to store the first user of the server. This user gets assigned in the System Administrator role. That enables them to setup all other users and to further configure the server. Please input all needed fields.
![Setup Storage](../../images/report-server-images/setup_admin_user_960.png)

## Further setup
When done with this sequence, you will land on the Reports page that lists the core assets of the server - the reports. The app adds a few sample reports to showcase the functionality.

As a next step, go to the Configuration page to configure a [send mail server]({%slug mail-server%}). This would enable the report scheduling functionality for all users.  The Configuration page is accessible in the up-right menu of the app UI.
