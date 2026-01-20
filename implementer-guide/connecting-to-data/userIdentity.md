---
title: UserIdentity
page_title: UserIdentity
description: UserIdentity
slug: useridentity
tags: useridentity,report server, report server agent
published: True
position: 800
---

# UserIdentity

[UserIdentity](https://docs.telerik.com/reporting/api/telerik.reporting.processing.useridentity) is designed to be used in web projects that utilize the Telerik Reporting REST API. It returns the main identity for this user, such as their username or authentication type. This property provides structured information about the user, such as Name, AuthenticationType, and authentication status, and offers a Context dictionary for custom data.

The code responsible for initializing the User Identity is located solely in the [ReportsControllerBase class](https://docs.telerik.com/reporting/api/telerik.reporting.services.webapi.reportscontrollerbase).

> In web projects, user identity is initialized through the HTTP context, which provides the necessary runtime information.

> In desktop applications, no such initialization mechanism is available, and therefore, the User Identity is not automatically initialized.

## UserIdentity in Report Server and Report Server Agent

### Report Server

The Report Server is a web application that requires user authentication. When our code triggers a viewer and reaches the GetUserIdentity() method, the user is already authenticated in the Report Server. As a result, GetUserIdentity() retrieves the username of the currently logged‑in user. This ensures that all subsequent operations are performed under the correct authenticated identity.

### Report Server Agent

On the legacy server(localhost:83), the Report Server Agent runs as a Windows Service therefore it does not provide the GetUserIdentity() method. As a result, retrieving the user identity through UserIdentity is not supported in this environment.

On the new server(localhost:81), the Report Server Agent will initialize the UserIdentity using the system user.

## Behavior Across Execution Scenarios

When a report is previewed through the Report Server UI, the UserIdentity value corresponds to the currently logged‑in user.

When the same report is executed by a Scheduled task, the application running it is not a web application, and therefore, no authenticated user context is available. As a result, UserIdentity is empty in this scenario.
