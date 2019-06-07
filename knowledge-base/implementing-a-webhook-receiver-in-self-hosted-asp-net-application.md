---
title: Implementing a webhook receiver in Self-Hosted Asp.Net application
description: This article elaborates on how to create a OWIN self-host console application for the WebApi that recives webhooks.
type: how-to
page_title: Implementing a webhook receiver in Self-Hosted Asp.Net application
slug: implementing-a-webhook-receiver-in-self-hosted-asp-net-application
position: 
tags: WebHook
ticketid: 1411427
res_type: kb
---

## Environment
<table>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server</td>
	</tr>
</table>

## Description
[Webhooks](https://en.wikipedia.org/wiki/Webhook) are user-defined HTTP callbacks which are usually triggered by some event, such as executing a data alert or modifying a report. When that event occurs, the report server makes an HTTP POST request to the URL configured for the webhook in order to notify the subscriber.

A step-by-step instructions on how to create and receive webhooks is provided in [Implement Webhooks](../implementer-guide/webhooks-implementation) documentation article. 

This knowledge base article is an example of implementing a self-hosted custom webhook receiver.

## Solution

Implementation of a webhook could be divided into two major steps:
### 1. Creating a Webhook

For these steps, follow the [Create Webhooks section](../implementer-guide/webhooks-implementation#create-webhooks) of the documentation.

### 2. Receive Webhooks

To implement a webhook receiver in your self hosted console application follow these steps:

1. Install the following Nuget package and their dependencies:
  - [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom);
  - [Microsoft.AspNet.WebApi.Owin](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Owin).

2. Initialize the custom webhook receiver in a new class called **Startup.cs**:

  ```C#
  public class Startup
  {
      // This code configures Web API. The Startup class is specified as a type
      // parameter in the WebApp.Start method.
      public void Configuration(IAppBuilder appBuilder)
      {
          // Configure Web API for self-host. 
          HttpConfiguration config = new HttpConfiguration();

          // Set the assembly resolver so that WebHooks receiver controller is loaded.
          WebHookAssemblyResolver assemblyResolver = new WebHookAssemblyResolver();
          config.Services.Replace(typeof(IAssembliesResolver), assemblyResolver);

          // Web API routes
          config.MapHttpAttributeRoutes();

          config.Routes.MapHttpRoute(
              name: "DefaultApi",
              routeTemplate: "api/{controller}/{id}",
              defaults: new { id = RouteParameter.Optional }
          );

          appBuilder.UseWebApi(config);

          // Initialize Custom WebHook receiver
          config.InitializeReceiveCustomWebHooks();
      }
  }
  ```
3. The receiver uses a shared **secret** to validate that the request comes from the report server. On the report server side the secret is set when creating the webhook. On the receiver it is provided by adding an application setting in the **App.config** file. The secret should be between 32 and 128 characters. For example:

  ```XML
  <appSettings>
    <add key="MS_WebHookReceiverSecret_Custom" value="12345678901234567890123456781012"/>
  </appSettings>   
  ```
The value is a comma-separated list of values matching the *{id}* values for which webhooks have been registered, for example:

  ```
  value="12345678901234567890123456781012, 12345=11111122222233333344444455555511"
  ```
The following example shows a webhook with a secret without an identifier:

  ```
  WebHookUri: "http://<receiver host>/api/webhooks/incoming/custom",
  Secret: "12345678901234567890123456781012",
  ```
The following example shows a webhook with a secret identified by an {id} parameter:

  ```
  WebHookUri: "http://<receiver host>/api/webhooks/incoming/custom/12345",
  Secret: "11111122222233333344444455555511",
  ```
4. Once a webhook request from the report server has been validated by a receiver, it is ready to be processed by user code. This happens inside a handler.

  ```C#
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
  
Report server will resend a webhook notification 3 times if a response is not generated within a handful of seconds. This means that your handler must complete the processing within that time frame in order not for it to be called again. If the processing takes longer, or is better handled separately then a [Queued Processing](https://media.readthedocs.org/pdf/aspnetwebhooks/stable/aspnetwebhooks.pdf) approach can be used.

## Notes
The report server webhooks implementation is based on [ASP.NET WebHooks](https://github.com/aspnet/aspnetwebhooks). Further information can be found in the official [Resources](https://github.com/aspnet/aspnetwebhooks#resources) and [Samples](https://github.com/aspnet/aspnetwebhooks#samples).
