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

The Report Server is a web application that requires user authentication. When rendering a report - either in the Report Server's web application or through its REST API - the operation is performed in an authentication context. As a result, GetUserIdentity() retrieves the username of the currently logged‑in user. This ensures that all subsequent operations are performed under the correct authenticated identity.

### Report Server Agent

When using Telerik Report Server for .NET Framework, the RSA operates as a Windows Service. Because Windows Services do not have an HttpContext, the system cannot determine the current user identity and therefore cannot initialize the internal model.

When using Telerik Report Server on .NET 8, the Report Server Agent runs as a web application that authenticates internally using a built‑in system user account. This internal account does not have a configured user name and cannot populate the internal model.

## Behavior Across Execution Scenarios

When a report is previewed through the Report Server UI, the UserIdentity value corresponds to the currently logged‑in user.

When the same report is executed by a Scheduled Task or Data Alert, it gets processed by the Report Server Agent, where the authenticated user context is not available or not initialized. As a result, the GetUserIdentity() function will return an empty string.

## See Also

* [UserIdentity in Telerik Reporting](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/expressions/expressions-reference/global-objects#useridentity)
