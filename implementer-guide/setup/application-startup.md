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
When the report server application is started it detects if it has the minimum configuration available to serve the assets management. If these configuration settings are not available, the app starts a two-page setup process for the user, assuming this is the person that installed the product. The pages are:

## Step 1/2: Setup storage
All Report Server assets including reports, scheduled tasks, and users need to be stored permanently. The supported target storages are File storage, MS SQL Server storage, and Redis storage. By default, the setup page offers the File storage which is basically a folder where all assets get stored as files. It is chosen by default as it does not require any additional tool installation, so it is perfect for test deployment and as well for production deployment, if the Report Server instance will not be highly utilized. For other cases including multi-instance setup one of the other options is a must. More info on each supported storage can be found in the article [Storage]({%slug storage-settings%}). The storage settings go into the Report Server configuration file called *ReportServerAdmin.config*

## Step 2/2: Register administrator
Once we have storage, it can be used to store the first user of the server. This user gets assigned in the System Administrator role so that he/she can setup all other users and configure the server. Please input all needed fields.

## Further setup
When finished, this sequence leads to the Reports page that lists the core assets of the server - the reports. A few sample reports get added to showcase the functionality. It is recommended to go to the Configuration page (accessible in the up-right menu of the RS UI) and configure a [send mail server]({%slug mail-server%}) so that users can utilize the report scheduling functionality.
