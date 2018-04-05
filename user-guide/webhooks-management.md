---
title: Webhooks Management
page_title: Webhooks Management
description: Webhooks Management
slug: webhooks-management
tags: webhooks,management
published: False
position: 720
---

# Webhooks Management

The **Webhooks** view is used to create and manage webhooks. Webhooks are user-defined HTTP callbacks which are usually triggered by some event, 
such as executing a data alert or modifying a report. When that event occurs, the report server makes an HTTP request to the URL configured for the webhook in order to notify the subscriber.

## Webhooks Grid

The **Webhooks** grid allows you to create, modify, and delete webhooks. The grid has the following fields:

-   **User** - the report server user which created the webhook. This field will be visible to **System Administrator** users only. For non-administrator users the grid displays only the current user's webhooks.

-   **Webhook URL** - the URL which will be called when an event occurs. An HTTP POST request is sent to the URL with information about what happened so that another web application can act accordingly.

-   **Secret** - the secret used to sign the body of the webhook request. Should be between 32 and 128 characters long. Report server uses a shared secret which is created as part of subscribing for events. The subscriber uses this shared secret to validate that the request comes from the report server.

-   **Filters** - the set of case-insensitive filters associated with a webhook. The filters indicate which events a webhook will be notified for. When no filters are specified, the webhook will be notified for all types of events.

    -   *reports* - events of this type are triggered when a report is added, edited, or deleted.

    -   *categories* - events of this type are triggered when a category is added, modified, or deleted.

    -   *connections* - events of this type are triggered when a data connection is added, modified, or deleted.

    -   *tasks* - events of this type are triggered when a scheduled task is added, modified, deleted, or executed.

    -   *alerts* - events of this type are triggered when a data alert is added, modified, deleted, or executed.

-   **Description** - an optional description of the webhook.

-   **Paused** - indicates whether the webhook is paused.

>Webhook notifications will not be sent if the user which created the webhook does not have **Read** access for the specific report server resource (report, data alert, etc.) which triggers the event.

## Receiving Webhooks

To implement a webhook receiver in your web application refer to the [Implement Webhooks]({%slug webhooks-implementation%}) page.