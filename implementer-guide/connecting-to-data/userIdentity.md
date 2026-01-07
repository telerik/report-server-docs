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

[UserIdentity](https://docs.telerik.com/reporting/api/telerik.reporting.processing.useridentity) represents the current user identity used when evaluating report expressions. It is automatically populated for web previews in the HTML5 Report Viewer and can be customized by overriding GetUserIdentity. When exporting reports programmatically, set [Telerik.Reporting.Processing.UserIdentity.Current](https://docs.telerik.com/reporting/api/telerik.reporting.processing.useridentity#Telerik_Reporting_Processing_UserIdentity_Current) to define the user context.

## UserIdentity Properties

To access the user identity in Telerik Reports, you can leverage the UserIdentity class provided by Telerik Reporting. This allows you to retrieve details such as the user's `name`, `authentication` status, and other `context-specific` information.

| Name | Description |
| ------ | ------ |
| AuthenticationType | Indicates the type of authentication used. Gets or sets a string value that specifies the authentication mechanism applied for the current user session (e.g., Cookie for server-based login or Bearer for token-based authentication) |
| Context | Provides access to the context collection for storing and retrieving user-specific objects |
| Current | Gets or sets the UserIdentity context that defines the user-specific information used during report processing and expression evaluation. |
| IsAuthenticated | Indicates whether the user has been authenticated |
| Name | It will return the name of the user |

## UserIdentity in Report Server and Report Server Agent

