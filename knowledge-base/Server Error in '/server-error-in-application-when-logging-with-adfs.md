---
title: Potentially dangerous RequestForm value was detected from the client when logging with ADFS
description: You might not be able to log with ADFS because ASP.NET might detect data in the request which is potentially dangerous
type: troubleshooting
page_title: Server Error in '/' Application when Logging with ADFS
slug: server-error-in-application-when-logging-with-adfs
position: 
tags: #reportserver, AzureAD
ticketid: 1549560
res_type: kb
---

## Environment
<table>
	<tbody>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® Report Server</td>
		</tr>
	</tbody>
</table>


## Description
The problem  is caused by a known issue with AD which is logged on our feedback portal - 
[Web.config error after authenticating with Active Directory](https://feedback.telerik.com/report-server/1516342-web-config-error-after-authenticating-with-active-directory). 

## Error Message
The **Potentially dangerous Request.Form in WSFederationAuthenticationModule.IsSignInResponse** error can be observed in the Event Viewer Log. 
In the application, you may see **Server Error in '/' Application**.

## Cause\Possible Cause(s)
ASP.NET has detected data in the request that is potentially dangerous because it might include HTML markup or script.
The data might represent an attempt to compromise the security of your application, such as a cross-site scripting attack. If this type of input is appropriate in your application, you can include code in a web page to explicitly allow it. 

## Workaround

 The workaround is adding the following **requestValidationMode="2.0"** setting in the web.config file which will remove the "potentially dangerous" exception:

````xml
<httpRuntime maxRequestLength="2097152" requestValidationMode="2.0"/> 
````


The Report Server's Web.config configuration file can be found in {reportServer_installDir}/Telerik.ReportServer.Web. For example, if you have installed the product with the default settings, you can find the file at the following path:

C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web

More details about the workaround can be found at the following StackOverflow thread - 
[Potentially dangerous Request.Form in WSFederationAuthenticationModule.IsSignInResponse](https://stackoverflow.com/questions/5443563/potentially-dangerous-request-form-in-wsfederationauthenticationmodule-issigninr).

