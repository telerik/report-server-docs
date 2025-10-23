---
title: Using Tokens for Authentication
page_title: Authenticate with Tokens against the Report Server .NET
description: "Learn how to use JWT Tokens to authenticate against the Telerik Report Server .NET instance."
slug: rs-net-token-authentication
tags: report, server, dotnet, token, authenticate
published: True
position: 25
---

# Configuring the Report Server for .NET for Authentication with JWT Tokens

Starting with [2025 Q4(11.3.25.1112)](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-2025-q4-11-3-25-1112) Telerik Report Server for .NET enhances security by letting you register custom JWT Tokens for all the [Users]({%slug users%}), including the [Guest User]({%slug guest-user%}). The tokens may be passed instead of user/password credentials from the Report Viewers for authentication against the Report Server .NET.

In this article, we will explain:
* how to add custom JWT Tokens letting Report Server Users connect to the Report Server .NET remotely;
* how the server utilizes the Tokens;
* how an authenticated user may share reports with the outside world.

## Mechanism

Report Server admins and users with proper permissions may add Tokens to each User, including the Guest User. Each Token may be used to authenticate remotely against Report Server for .NET with the permissions of the corresponding User the Token belongs to. The Token has expiration time selected by the User:

![image]()


## Guest User

## Sharing Reports

Each generated report preview may be shared by the corresponding user with the outside world:

![image]()

The shared link contains an authomatically genarated JWT Token belonging to the Guest User. This means that the access of the shared document is through the Guest User. 

## Limitations

* Each Token grants the permissions of the User it belongs to.
* The Tokens are restricted to be used by Report Viewers for authentication agains the Report Server for .NET.

## See Also

* [Report Server for .NET Overview]({%slug coming-soon%})
* [Report Server Users]({%slug users%})
* [Guest User]({%slug guest-user%})