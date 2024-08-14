---
title: Using Microsoft Entra ID
page_title: Single Sing-On with Microsoft Entra ID
description: "Learn how to setup the Single Sign-On (SSO) functionality in Microsoft Entra ID and use it to authenticate against the Telerik Report Server instance."
slug: using-microsoft-entra-id
tags: azure,microsoft,entra,id
published: True
position: 201
---

# Configuring the Report Server for .NET Single Sign-On Functionality using Microsoft Entra ID

[Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/) is a cloud-based identity and access management service that can be used for authentication in the Telerik Report Server for .NET. 

In this article, we will explain how to set up and enable the Microsoft Entra ID authentication for the users of the Telerik Report Server for .NET. Besides the enhanced authentication security, this approach also improves the user experience, because the users who are already registered in Microsoft Entra will be able to log into Report Server Manager UI without entering their login credentials each time.

## Prerequisites

- Telerik Report Server installation with at least one administrator account and enabled **https** site binding in its Internet Information Services registration.
- An Azure account with Active Directory support.

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

1. Add a Redirect URL `http://localhost:81/signin-oidc`.

	![An image of how to configure a redirect URL and the token settings for authentication between the Report Server and Azure](../images/rs-net-images/microsoft-entra-id-authentication-redirect-and-token-settings-step.png)

1. Click on **Certificates & secrets** in the expanded **Manage** dropdown in the menu on the left.
1. On the **Certificates & secrets** page, click on the **New client secret** button.

	![An image of how to trigger the creation of new client secret in the Azure portal](../images/rs-net-images/microsoft-entra-id-creating-client-secret-step.png)

	> Once the secret is created, copy and save the secret value as it will be used in the Report Server later. Note that you can do this only once, otherwise another secret should be created and its value used.

1. Go to the installation folder of the Telerik Report Server for .NET e.g. `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web.NET`.
1. Open the `appsettings.json` file in a text editor and add the following (replacing the secret from the example below with your secret):

	````JSON
"ExternalLogin":{
	"EntraId":{
		"ClientSecret":"mMr8Q~da2a55f0-1e7f-4f9d-bff0-dd193582218d"
	}
}
````


### 3. Enabling Microsoft Entra ID Authentication in the Telerik Report Server for .NET 

1. Open the Telerik Report Server for .NET in the browser. The default URL is `http://localhost:81/`.
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
