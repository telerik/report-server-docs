---
title: Cors
page_title: Cors
description: Cors Settings
slug: cors
tags: cors,settings
published: True
position: 650
---

# CORS

This page allows to configure the Cross-Origin Resource Sharing (CORS) settings of the Report Server web application. CORS is configured during the application startup by the CORS extensions provided by the [Microsoft.Owin](https://www.nuget.org/packages/Microsoft.Owin/) middleware. The CORS setting can have one of the following states:

- *Enabled* - the CORS policy applied to the web application will include all the origins listed in the **Origins** text area. The policy allows any header and any method to be used. Every origin must be placed on a separate row. The origin should contain scheme, hostname and optionally - a port, example: http://localhost:57615.

- *Disabled* - the CORS policy applied to the web application will not allow any header, method or origin to be used for requesting Report Server's resources.

- *Not Set* - the application will not have any CORS policy applied. In this case the CORS behavior can be controlled from the application configuration file. In order to have CORS working while using *Not Set* option, consider installing the [IIS CORS Module](https://www.iis.net/downloads/microsoft/iis-cors-module). This is a tool developed by Microsoft's IIS Team and allows to configure CORS through the web.config file. A sample snippet that configures CORS to allow all origins, all methods and specifically OPTIONS method is shown below:

```
    <system.webServer>
    ...
    	<cors enabled="true" failUnlistedOrigins="true">
    		<add origin="*" allowed="true">
    			<allowHeaders allowAllRequestedHeaders="true">
    				<add header="*" />
    			</allowHeaders>
    			<allowMethods>
    				<add method="OPTIONS" />
    			</allowMethods>
    		</add>
    	</cors>
    </system.webServer>
```

When the CORS settings are modified and configuration settings are saved, the application prompts that it needs to be restarted in order to apply the new CORS settings. After confirming, the application will be automatically restarted and the Configuration page will be reloaded.
