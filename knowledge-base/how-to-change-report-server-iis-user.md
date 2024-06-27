---
title: How to Create a limited IIS User for Report Server and Service Agent
description: this tutorial shows how to use a lower privlidged user to host Report Server in IIS
type: how-to
page_title: How to change IIS user for Report Server and Service Agent
slug: how-to-change-report-server-iis-user
tags: report server, iis, user permissions, iis permissions
res_type: kb
---

## Environment

|  |  |
|---------|-----------------|
| Product | Progress® Telerik® Report Server |
| Version | 10.1.24.514 |

## Description

This tutorial will show you how to change the Report Server's IIS application pool and service agent to use an identity with limitd permissions.

## Solution

1. Create a new **Windows** User with limited permissions.

    ![](images/change-iis-user/1-add-new-user.png)

    *For more help, see [Microsoft Docs - Manage User Accounts in Windows](https://support.microsoft.com/en-us/windows/manage-user-accounts-in-windows-104dc19f-6430-4b49-6a2b-e4dbd1dcdf32).*

2. Go to Telerik Report Server's installation directory (*C:\Program Files (x86)\Progress\Telerik Report Server*) and give `RSUser` full access permissions to the **Telerik.ReportServer.Web** and **Services** subfolders.

      ![](images/change-iis-user/2-add-permissions-to-rsuser.png)

      *Ensure the user does not have read or write permissions to any other folders. For more help, see [Microsoft Q&A - How do I set up user account and manage permissions](https://learn.microsoft.com/en-us/answers/questions/1389054/how-do-i-set-up-user-accounts-and-manage-permissio).*

3. Open Internet Information Services (IIS) Manager (`Windows Key` + `R` to open the Run window, then enter `inetmgr`).

4. In the left column, expand the machine's node and select **Application Pools**. Right-click on the `TelerikReportServer` application pool and select **Advanced Settings** from the context menu.

    ![](images/change-iis-user/2.5-locate-application-pool.png)

5.	Select the **Identity** item and click on the ellipsis button:

    ![](images/change-iis-user/3-open-iis-apppool-advanced-settings.png)

6.	Select **Custom account**, click **Set…** and enter the name of the newly created user (e.g. `RSUser`) and its password:

    ![](images/change-iis-user/4-set-iis-apppool-identity.png)

7. Right-click on the `TelerikReportServer` application pool and select **Recycle...** from the context menu.

8. Open the Report Server Manager application in the web browser to confirm it is working with the new user identity.

8.	Open Windows's Services app (`Windows Key` + `R` to open the Run window, then enter `services.msc`).

9.	Scroll to `Telerik.ReportServer.ServiceAgent` service instance:

    ![](images/change-iis-user/5-services-panel.png)

10.	Double-click to show the service's **Properties** panel. Select the **Log On** tab.

11.	Click on **This account** and enter the new user name (e.g. `.\RSUser`) and its password:

    ![](images/change-iis-user/6-services-set-local-user.png)

12.	Right-click on `Telerik.ReportServer.ServiceAgent` and select **Restart** to restart the service with the new user.

13. Ensure it is working by running a **scheduled task** or a **data alert** from Report Server Manager web UI.

> Additional Actions: Consider adding the local user to databases used by Report Server data connections that utilize Windows Credentials login permissions.