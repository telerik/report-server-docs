---
title: Implement Webhooks
page_title: Implement Webhooks
description: Implement Webhook Receivers
slug: webhooks-implementation
tags: webhooks,implementation
published: True
position: 700
---

# Implement Webhooks

Webhooks are user-defined HTTP callbacks which are usually triggered by some event, such as executing a data alert or modifying a report. 
When that event occurs, the report server makes an HTTP POST request to the URL configured for the webhook in order to notify the subscriber.

## Create Webhooks

### Webhooks Grid
 
The **Webhooks** grid provides a simple user interface to create, modify, or delete webhooks. For an overview of the grid refer to the [Webhooks Management]({%slug webhooks-management%}) page.

### POST Request

Webhooks can also be managed by making a POST request to the report server API. This approach offers advanced webhook configuration options such as setting custom headers and properties 
to the HTTP callbacks made when an event occurs. To successfully make a POST request which creates a new webhook follow these steps:

1. Authenticate with the report server.
	```
		function login(username, password) {
			var serverHost = "http://<report server host>:<port>/";
			var serverApi = serverHost + "api/reportserver/";
			var accessToken = "";
		
			$.ajax({
				type: "POST",
				url: serverHost + "Token",
				async: false,
				data: {
					grant_type: "password",
					username: username,
					password: password
				}
			})
			.done(function (data, textStatus, jqXHR) {
				accessToken = data.access_token;
			})
			.fail(function (xhr, status, error) {
				window.alert(xhr.status + ": " + error);
			});
		
			return accessToken;
		}
	```
	>Webhook notifications will not be sent if the user which created the webhook does not have **Read** access for the specific report server resource (report, data alert, etc.) which triggers the event.
2. Create a webhook with specific configuration.
	```
		function subscribe() {
            var accessToken = login("<username>", "<password>");

            $.ajax({
                type: "POST",
                beforeSend: function (request) {
                    request.setRequestHeader('Authorization', 'Bearer ' + accessToken);
                },
                url: "http://<report server host>:<port>/api/webhooks/registrations",
                data: JSON.stringify({
                    WebHookUri: "http://<receiver host>/api/webhooks/incoming/custom/{id}",
                    Secret: "12345678901234567890123456781012",
                    Description: "Notify me for events triggered by reports, scheduled tasks, and data alerts!",
					Filters: ["reports","tasks","alerts"]
                }),
                contentType: "application/json; charset=utf-8",
                dataType: "json",
                success: function (data, status) { alert(status); },
                failure: function (errMsg) { alert(errMsg); }
            });
            return false;
        }
	```
	The *{id}* is an optional identifier which can be used to identify a particular webhook receiver configuration. This
	can be used to register *N* webhooks with a particular receiver. For example, the following three URLs can be used to
	register for three independent webhooks:
	```
		http://<receiver host>/api/webhooks/incoming/custom
		http://<receiver host>/api/webhooks/incoming/custom/12345
		http://<receiver host>/api/webhooks/incoming/custom/54321
	```
	
## Receive Webhooks

To implement a webhook receiver in your web application follow these steps:

1. Install the [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) Nuget package and its dependencies.
2. Initialize the custom webhook receiver:
	```
		public static class WebApiConfig
		{
			public static void Register(HttpConfiguration config)
			{
				// Web API configuration and services

				// Web API routes
				config.MapHttpAttributeRoutes();

				config.Routes.MapHttpRoute(
					name: "DefaultApi",
					routeTemplate: "api/{controller}/{id}",
					defaults: new { id = RouteParameter.Optional }
				);

				// Initialize Custom WebHook receiver
				config.InitializeReceiveCustomWebHooks();
			}
		}
	```
3. The receiver uses a shared **secret** to validate that the request comes from the report server. On the report server side the secret is set when creating the webhook. 
On the receiver it is provided by adding an application setting in the *web.config* file. The secret should be between 32 and 128 characters. For example:

	```
		<appSettings>
		  <add key="MS_WebHookReceiverSecret_Custom" value="12345678901234567890123456781012"/>
		</appSettings>		
	```
	The *value* is a comma-separated list of values matching the *{id}* values for which webhooks have been registered, for example:
	```
		value="12345678901234567890123456781012, 12345=11111122222233333344444455555511"
	```
	The following example shows a webhook with a secret without an identifier:
	```
		WebHookUri: "http://<receiver host>/api/webhooks/incoming/custom",
		Secret: "12345678901234567890123456781012",
	```
	The following example shows a webhook with a secret identified by an *{id}* parameter:
	```
		WebHookUri: "http://<receiver host>/api/webhooks/incoming/custom/12345",
		Secret: "11111122222233333344444455555511",
	```
	
4. Once a webhook request from the report server has been validated by a receiver, it is ready to be processed by user code. This happens inside a handler.
	```
		public class CustomWebHookHandler : WebHookHandler
		{
			public CustomWebHookHandler()
			{
				this.Receiver = CustomWebHookReceiver.ReceiverName;
			}

			public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
			{
				// Get data from WebHook
				CustomNotifications data = context.GetDataOrDefault<CustomNotifications>();

				// Get data from each notification in this WebHook
				foreach (IDictionary<string, object> notification in data.Notifications)
				{
					// Process data
				}

				return Task.FromResult(true);
			}
		}
	```

Report server will resend a webhook notification 3 times if a response is not generated within a handful of seconds. This means that your handler must complete the processing within that time frame in order not for it to be called again.
If the processing takes longer, or is better handled separately then a [Queued Processing](https://media.readthedocs.org/pdf/aspnetwebhooks/stable/aspnetwebhooks.pdf) approach can be used.
	
>The report server webhooks implementation is based on [ASP.NET WebHooks](https://github.com/aspnet/aspnetwebhooks). 
>Further information can be found in the official [Resources](https://github.com/aspnet/aspnetwebhooks#resources) and [Samples](https://github.com/aspnet/aspnetwebhooks#samples).