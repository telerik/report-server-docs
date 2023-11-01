---
title: Webhooks Management
page_title: Webhooks Management
description: Webhooks Management
slug: webhooks-management
tags: webhooks,management
published: True
position: 720
---

# Webhooks Management

The __Webhooks__ view is used to create and manage webhooks. Webhooks are user-defined HTTP callbacks that are usually triggered by some event, such as executing a data alert or modifying a report. When that event occurs, the report server makes an HTTP request to the URL configured for the webhook in order to notify the subscriber.

## Webhooks Grid

The __Webhooks__ grid allows you to create, modify, and delete webhooks. The grid has the following fields:

* __User__ - the report server user who created the webhook. This field will be visible to __System Administrator__ users only. For non-administrator users, the grid displays only the current user's webhooks.
* __Webhook URL__ - the URL that will be called when an event occurs. An HTTP POST request is sent to the URL with information about what happened so that another web application can act accordingly.
* __Secret__ - the secret used to sign the body of the webhook request. Should be between 32 and 128 characters long. The Report Server uses a shared secret which is created as part of subscribing for events. The subscriber uses this shared secret to validate that the request comes from the report server.
* __Filters__ - the set of case-insensitive filters associated with a webhook. The filters indicate which events a webhook will be notified for. When no filters are specified, the webhook will be notified for all types of events.

	+ *reports* - events of this type are triggered when a report is added, edited, or deleted.
	+ *categories* - events of this type are triggered when a category is added, modified, or deleted.
	+ *connections* - events of this type are triggered when a data connection is added, modified, or deleted.
	+ *tasks* - events of this type are triggered when a scheduled task is added, modified, deleted, or executed.
	+ *alerts* - events of this type are triggered when a data alert is added, modified, deleted, or executed.

* __Description__ - an optional description of the webhook.
* __Paused__ - indicates whether the webhook is paused.

> Webhook notifications will not be sent if the user who created the webhook does not have __Read__ access for the specific report server resource (report, data alert, etc.) that triggers the event.

## Receiving Webhooks

To implement a webhook receiver in your web application refer to the [Implement Webhooks]({%slug webhooks-implementation%}) page.

## Telerik Report Server Learning Resources

* [Telerik Report Server Homepage](https://www.telerik.com/report-server)
* [Telerik Report Server Installation]({%slug installation%})
* [Telerik Report Server User Management]({%slug user-management%})
* [Connecting to Data with Telerik Report Server]({%slug connecting-to-data%})
* [Telerik Report Server License Agreement](https://www.telerik.com/purchase/license-agreement/report-server)
