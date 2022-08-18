---
title: Guest user
page_title: Guest user
description: Explains the Guest user feature and its purpose and limitations
slug: guest-user
tags: users,guest,share,embed
published: True
position: 400
---

# Guest user
The Guest user is a built-in user account That is created upon the initial setup of the Telerik Report Server. The Guest's purpose is to be used for report document preview and sharing, either using a sharing link to a report, a report viewer control embedded in a client application, or the reports API.

## Guest User Administration
The Guest user is not enabled by default. To enable it, navigate to the _User Management -> Users_ view, select the Guest user from the list of users and turn on the _Enabled_ switch.
By default, this user has _Read_ permission on all reports in all categories. If some reports or categories should not be generally accessible, delete the default permission and substitute it with more specific _Read_ permissions.
![Enable the Guest user](../../images/report-server-images/enable_guest_user.png)

## Usage
###	Share a report that resides on the Report Server with a URL
Report Server's API provides a method that serves a report by specified category, report name, and report revision. The format of the method is 
*{serverUrl}/report/share/{category}/{reportName}/{revision}*. The _revision_ parameter can be omitted, 
which will result in displaying the last revision of the specified report. In case the Guest account is disabled, a 403-Forbidden error is returned.

###	Display a server report in an embedded Report Viewer control
The Guest account can be used for authentication against the Report Server when you want to embed any Report Viewer displaying server reports into a user application.
To do this no authentication token is provided and Guest user authorization is done on the server. 
You can read more in the (%slug integration-with-report-viewers%) article.

## Limitations of the Guest user
-	Cannot be edited - since it doesn't have any user-related fields except *username*, the _Edit_ button is disabled when the Guest user is selected.

-	Cannot be used to log in to Telerik Report Server manager or API.

-	Cannot have any permission other than _Read_. It cannot modify, create or delete reports.

-	Permission scope is limited to Reports - based on the previous limitations, the Guest user's Read permission can only have a report-related scope.

-	Cannot have any Roles - the Guest can only read reports and since a role can have virtually any permission, adding the Guest user to a role is not permitted.

- Cannot be used to perform operations with Report Server resources using its API as they require passing an access token. The only allowed method is GET _{serverUrl}/report/share/{category}/{reportName}/{revision}_.
