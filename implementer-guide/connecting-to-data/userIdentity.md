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

## UserIdentity in Report Server and Report Server Agent

### Report Server

Since the Report Server is implemented as a web application, the UserIdentity property is fully supported and functions correctly in this context. By design, the Report Server integrates with the underlying web infrastructure, which allows it to consistently provide accurate user identity information across all reporting operations.

### Report Server Agent

On the legacy server(localhost:83), the Report Server Agent runs as a Windows Service. In this configuration, the UserIdentity property is not initialized.

On the new server, the Report Server Agent will initialize the UserIdentity using the system user.
