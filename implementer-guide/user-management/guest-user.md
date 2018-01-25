---
title: Guest user
page_title: Guest user
description: Guest user
slug: guest-user
tags: users,guest
published: True
position: 400
---

# Guest user

Guest user is a special built-in user which is created upon the initial setup of Telerik Report Server. The Guest's purpose is to be used for read-only connections to report server, either using the reports API or sharing a link to a report.

### Features and limitations of the Guest user

-	Cannot be edited - since it doesn't have any user-related fields except *username*, the **Edit** button is disabled when the Guest user is selected. Its Enabled/Disabled status can be changed using a button in the Permissions tab.

-	Cannot be used to log in - the Guest user doesn't have a password, so it cannot be used to log in into Telerik Report Server.

-	Cannot have any permission other than **Read** - the Guest user is a read-only user, hence it cannot modify, create or delete reports.

-	Permission scope is limited to Reports - based on the previous limitations, the Guest user's Read permission can only have a report-related scope.

-	Cannot have any Roles - the Guest can only read reports and since a role can have virtually any permission, adding the Guest user to a role is not permitted.

### Usage

-	Share a report that resides in Report Server - Report Server's API provides a method that serves a report by specified category, report name and report revision. The format of the method is *{serverUrl}/report/share/{category}/{reportName}/{revision}*. The Revision parameter can be omitted, which will result of displaying the last revision of the specified report. In case the Guest account is disabled, a 403-Forbidden error is returned.

-	Access the report REST service API using the HTML5 viewer - the Guest account can be used for authentication against the Report Server when you want to connect the HTML5 Report Viewer to its report service API. Please note that in this case no authentication token is required and Guest user validation is done on the server. You can read more [here](https://docs.telerik.com/reporting/html5-report-viewer-howto-use-it-with-reportserver "Configuring the HTML5 Report Viewer to work with Report Server").
