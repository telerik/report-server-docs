---
title: Using Microsoft Entra ID on Linux
page_title: Single Sign-On with Microsoft Entra ID on Linux
description: "Learn how to setup the Single Sign-On (SSO) functionality in Microsoft Entra ID and use it to authenticate against the Telerik Report Server instance that is hosted on Linux/Container."
slug: using-microsoft-entra-id-linux
tags: azure,microsoft,entra,id,linux
published: True
position: 202
---

# Configuring the Report Server for .NET Single Sign-On Functionality using Microsoft Entra ID for Linux/Container

[Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/) is a cloud-based identity and access management service that can be used for authentication in the Telerik Report Server for .NET. 

In this article, we will explain how to set up and enable the Microsoft Entra ID authentication for the users of the Telerik Report Server for .NET. Besides the enhanced authentication security, this approach also improves the user experience, because the users who are already registered in Microsoft Entra will be able to log into Report Server Manager UI without entering their login credentials each time.

## Prerequisites

- Telerik Report Server installation with at least one **administrator** account.
- An Azure account with Microsoft Entra ID support.

> In case you are unfamiliar with the process of using Microsoft Entra ID, we recommend checking out the [Set up Microsoft Entra ID](https://learn.microsoft.com/en-us/mem/intune/industry/education/tutorial-school-deployment/set-up-microsoft-entra-id) article.

### 1. Create a Microsoft Entra ID Tenant

1. Navigate to the [Microsoft Azure Home page](https://portal.azure.com/#home).
1. From the menu in the top left corner of the page, select **Microsoft Entra ID**.
1. From the *Overview* page that is displayed, click on **Manage Tenants**.

	![An image of where the Manage Tenant button is located in the Azure portal](../images/rs-net-images/microsoft-entra-id-manage-tenants-step.png)

1. Click on the **Create** button on the **Manage Tenants** page

	![An image of where the Create button is located on the Manage Tenants page in the Azure portal](../images/rs-net-images/microsoft-entra-id-create-tenant-step.png)

1. On the **Create a tenant** page, choose `Microsoft Entra ID` as the tenant type (it should be selected by default).

	![An image of the Create a tenant page with Microsoft Entra ID as the selected type](../images/rs-net-images/microsoft-entra-id-select-tenant-type-step.png)

1. Click on **Next: Configuration >** and type Organization name (for example, `Report Server Tenant`) and Initial Domain Name (e.g. `ReportServerNetDomain`).

	![An image of the configuration step of creating a tenant with sample directory details](../images/rs-net-images/microsoft-entra-id-tenant-configuration-step.png)

1. Click on **Next: Review + create >** and if the configuration is correct, a green message notifying that the validation has passed will be displayed.

	![An image of the review and create step of creating a tenant](../images/rs-net-images/microsoft-entra-id-tenant-review-step.png)

1. Click on **Create** and then fill in the Captcha (it will take a minute or two to complete the process once it has been submitted).

### 2. Registering the Telerik Report Server for .NET Application

1. If the steps from the previous section were completed successfully, the following green message should appear above the Captcha: `Tenant creation was successful. Click here to navigate to your new tenant: Report Server Tenant`. The text - `Report Server Tenant` will be your chosen organization name and there will be a link to the **Report Server Tenant Overview** page. 

	> If you are not on the **Report Server Tenant Overview** page, then go to the top left `Menu` >> `Microsoft Entra ID` >> click `Add` >> `App Registration`.
	
1. Register the application by choosing `Add` > `App registration`.

	> Add **Report Server Application**, for example, as a name, leave the rest options to be the default, and click `Register`.
 
	![An image of the step where the Report Server for .NET application is registered in Azure](../images/rs-net-images/microsoft-entra-id-app-registration-step.png)

1. Expand the **Manage** dropdown in the menu on the left and choose **Authentication**.
1. Click on `Add Platform` >> `Web` >> Tick the `ID Tokens` checkbox, then click on ***Configure*.

	![An image of how to open the authentication page for the Report Server application in Azure](../images/rs-net-images/microsoft-entra-id-authentication-step.png)

1. Add a Redirect URL `http://localhost:82/signin-oidc`.

	![An image of how to configure a redirect URL and the token settings for authentication between the Report Server and Azure](../images/rs-net-images/microsoft-entra-id-authentication-redirect-and-token-settings-step.png)

1. Click on **Certificates & secrets** in the expanded **Manage** dropdown in the menu on the left.
1. On the **Certificates & secrets** page, click on the **New client secret** button.

	![An image of how to trigger the creation of new client secret in the Azure portal](../images/rs-net-images/microsoft-entra-id-creating-client-secret-step.png)

	> Once the secret is created, copy and save the secret value as it will be used in the Report Server later. Note that you can do this only once, otherwise another secret should be created and its value used.


## 3. EntraID Setup on a local Telerik Report Server for .NET installation on Linux

1. Download the archive `Telerik_ReportServer_Net_NonWindows_{Report Server version}.zip` from [your Telerik account](https://www.telerik.com/account/downloads/product-download?product=REPSERVER).
1. Unzip the archive. The content gets deployed in two folders `ReportServer` and `ReportServiceAgent`.
1. Open the `Powershell` and navigate to the subfolder `ReportServer`.
1. Run the command `docker build -t telerik-report-server:local .` in _Powershell_ to build the Report Server Manager image.
1. Navigate to the subfolder `ReportServiceAgent`.
1. Run the command `docker build -t telerik-report-server-agent:local .` in _Powershell_ to build the Report Server ServiceAgent image.
1. Navigate to the subfolder `ReportServer\docker-configs`.
1. Open the file `docker-compose.yml` in a text editor like _Notepad++_ and edit its content. Delete everything between the lines `services:` and `  storage:`. Before the line `    environments` include the next lines:

	````yaml

	  ports:
	    - "1433:1433"
````

	The tabulation is essential and should be preserved. Here is the final content of the `docker-compose.yml` file:

	````yaml
services:

	storage:
	  image: "mcr.microsoft.com/mssql/server:2019-latest"
	  restart: always
	  ports:
	    - "1433:1433"
	  environment:
	    - SA_PASSWORD=place_your_sa_password_here
	    - ACCEPT_EULA=Y
	  volumes: 
	    - mssql-storage:/var/opt/mssql

	volumes:
	mssql-storage:
````


	Save the modified file.

1. Run the command `docker-compose up` in _Powershell_ to execute the above script to create and run the MsSqlServer Docker container we are going to use as Report Server Storage.
1. Open `MSSQL Management Studio` and _Login_ with the following parameters:

	* _Server_  : `localhost`
	* _User_    : `sa`
	* _Password_: `place_your_sa_password_here` (this is the argument _SA_PASSWORD_ from the above script file. You may change it as required.)

1. Add the database named `reportserver`. After successfully creating the database, you may close the management studio.
1. Stop the current process in _Powershell_, for example, with the key combination `Ctrl+C`.
1. Go back to the text editor with the opened file `docker-compose.yml` and restore its original content:

	````yaml
services:

	# template configuration of Report Server.
	# Includes sample config for /app/Data File Storage.
	telerik-report-server:
	  env_file:
	    - mssql_storage.env
	  image: telerik-report-server:local
	  restart: always
	  ports:
	    - "82:80"
	  depends_on: 
	    - storage

	# template configuration of Report Server Agent.
	# Includes sample config for /app/Data File Storage.
	telerik-report-server-agent:
	  environment:
	    - Agent__Name=FirstAgent,
	    - Agent__Address=http://telerik-report-server-agent:80
	  env_file:
	    - mssql_storage.env
	  image: telerik-report-server-agent:local
	  restart: always
	  depends_on:
	    - storage

	storage:
	  image: "mcr.microsoft.com/mssql/server:2019-latest"
	  restart: always
	  environment:
	    - SA_PASSWORD=place_your_sa_password_here
	    - ACCEPT_EULA=Y
	  volumes: 
	    - mssql-storage:/var/opt/mssql

	volumes:
	mssql-storage:
````


	Save the file.

1. Update the `telerik-report-server` information in the same file by adding the `ExternalLogin__EntraId__ClientSecret` environment attribute as shown below:

	````yaml
services:

	# template configuration of Report Server.
	# Includes sample config for /app/Data File Storage.
	telerik-report-server:
	  env_file:
	    - mssql_storage.env
	  image: telerik-report-server:local
	  restart: always
	  ports:
	    - "82:80"
	  depends_on: 
	    - storage

	# template configuration of Report Server Agent.
	# Includes sample config for /app/Data File Storage.
	telerik-report-server-agent:
	  environment:
	    - Agent__Name=FirstAgent,
	    - Agent__Address=http://telerik-report-server-agent:80
	    - ExternalLogin__EntraId__ClientSecret=HZq8Q~j9iO0Mr.WDn1U9IMHZClsacsWz3DTdlmgYjaOH
	  env_file:
	    - mssql_storage.env
	  image: telerik-report-server-agent:local
	  restart: always
	  depends_on:
	    - storage

	storage:
	  image: "mcr.microsoft.com/mssql/server:2019-latest"
	  restart: always
	  environment:
	    - SA_PASSWORD=place_your_sa_password_here
	    - ACCEPT_EULA=Y
	  volumes: 
	    - mssql-storage:/var/opt/mssql

	volumes:
	mssql-storage:
````

	Change the client secret with the one from the Entra ID setup in the Azure portal.

1. Go back to the _Powershell_ environment and execute the above _yaml_ file with the same command `docker-compose up`. This should run the Report Server Manager and ReportServer.ServiceAgent for .NET.
1. Navigate to `localhost:82` in the browser to open the Report Server Manager for .NET.

### 4. Enabling Microsoft Entra ID Authentication in the Telerik Report Server for .NET 

1. Open the Telerik Report Server for .NET in the browser. The default URL is `http://localhost:82/`.
1. Navigate to the **Configuration** page and select the **Authentication** tab.

	![An image of the Report Server for .NET Application's Configuration page on the Authentication tab](../images/rs-net-images/microsoft-entra-id-rs-net-configuration-authentication-settings.png)

1. Enable the `Microsoft Entra ID Provider`.
1. In the **Instance** field, use the URL - `https://login.microsoftonline.com/`.
1. In the **Domain** field, use the one from [step 5 in the Create a Microsoft Entra ID Tenant section](#1-create-a-microsoft-entra-id-tenant) and add it as a URL, for example - `https://ReportServerNetDomain.onmicrosoft.com/`.
1. Open the [Microsoft Azure Portal](https://portal.azure.com/) to get the `Tenant ID`:

	* From the menu in the top left corner of the page, select **Microsoft Entra ID**.
	* The `Tenant ID` can be copied from the **Basic Information** table in the center of the page.

1. Open the [Microsoft Azure Portal](https://portal.azure.com/) to get the `Client ID`:

	* From the menu in the top left corner of the page, select **Microsoft Entra ID**.
	* Expand the `Manage` dropdown >> `App Registrations` >> `All Applications`.
	* Click on the application name e.g. `Report Server Application` (defined in the previous section).
	* Copy the Application (client) ID and add it to the Report Server in the Client ID field.

		![An image of the Report Server Application page in the Azure portal where the application(client) ID is located](../images/rs-net-images/microsoft-entra-id-application(client)-id-location.png)

	* Click on the `Save Changes` button in the Report Server for .NET's Configuration page (a message that a manual restart of the service is required will appear on the screen).
	* The restart can be performed from the IIS Manager >> Application Pools >> Right-click on the Telerik Report Server for .NET site and choose `Recycle`.	

1. Once the service is manually restarted, log in with a user that has an administrator role and go to `User Management`.
1. Click on the `Add New User` button:

	* Select the `Authentication Provider` to be `EntraId`.
	* Add a username.
	* Add the domain name login email e.g. `username@mycompany.com.`
	* Choose a User Role and save the changes.

	![An image demonstratig how to create an user with EntraID authentication in the Report Server for .NET Application](../images/rs-net-images/microsoft-entra-id-rs-new-user-with-entraid-auth-provider.png)

1. Log out and from the Login page, click on the blue `Microsoft Entra ID` button.

	![An image demonstratig how the Report Server for .NET Login page looks when Microsoft Entra ID is enabled](../images/rs-net-images/microsoft-entra-id-login-page-with-enabled-entraid.png)

1. If all instructions were correctly applied, you should now be successfully logged in with your **EntraID** automatically. 

## See Also

* [What is Microsoft Entra ID?](https://learn.microsoft.com/en-us/entra/fundamentals/whatis) 
* [Set up Microsoft Entra ID](https://learn.microsoft.com/en-us/mem/intune/industry/education/tutorial-school-deployment/set-up-microsoft-entra-id)
* [Microsoft Entra ID Training](https://learn.microsoft.com/en-us/training/browse/?resource_type=module&expanded=entra&products=entra-id)
* [Installing ReportServer.NET on Docker Container]({%slug dotnet-installation-on-docker-container%})
