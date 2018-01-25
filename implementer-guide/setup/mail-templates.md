---
title: Mail Templates
page_title: Mail Templates
description: Mail Templates
slug: mail templates
tags: mail, templates, configuration
published: True
position: 500
---

# Mail Templates

Mail templates define the text which is sent via e-mail to the Report Server users for various reasons.

## Template Types

### Reset Password

Specifies the mail template used by the Report Server when sending a 'reset password' link in case a local user has forgotten his password. The mail template must contain the {link} variable as it will provide the link for the user to the 'reset password' page.

### Activate Account

Specifies the mail template sent to a new local user so that he/she can activate his/her account. The mail template must contain the {link} variable as it will provide a link for the user to the account activation page.

### Scheduled Task Attachment

Specifies the default mail template used by the scheduling service when sending an e-mail with the generated report document. You can configure a more specific template for this action in the New/Edit Scheduled Task dialog.
The variables which can be used only in this template type are:

-   {FirstName} - the first name of the user.

-   {LastName} - the last name of the user.

### Scheduled Task Attachment External

Specifies the mail template used by the scheduling service when sending an e-mail with the generated report document to an external user.

### Scheduled Task Error

Specifies the mail template sent by the scheduling service when there are errors during the report document generation. It might be a report processing error or general task scheduler error while trying to executed the scheduled task. If despite the errors a document has been generated then it will be sent as an attachment.
The variables which can be used only in this template are:

-   {Errors} - the errors that have occurred during the scheduled task execution.

## Common Variables

Mail variables common for all **Scheduled Task** templates:

-   {ReportName} - the name of the report document.

-   {TaskName} - the name of the scheduled task.

Mail variables common for all **Scheduled Task** templates with a generated report document (i.e. templates with an attachment):

-   {DocumentFormat} - the specified in the scheduled task rendering format.

-   {StartTime} - start time of the report document generation.

-   {StartTmeShort} - start time of the report document generation formatted with the **short time pattern** of the operating system.

-   {StartTimeLong} - start time of the report document generation formatted with the **long time pattern** of the operating system.

-   {StartDate} - start date of the report document generation formatted with the **short date** pattern of the operating system.

-   {StartDateLong} - start date of the report document generation formatted with the **long date** pattern of the operating system.

-   {EndTime} - end time of the report document generation.

-   {EndTimeShort} - end time of the report document generation formatted with the **short time pattern** of the operating system.

-   {EndTimeLong} - end time of the report document generation formatted with the **long time pattern** of the operating system.

-   {EndDate} - end date of the report document generation formatted with the **short date pattern** of the operating system.

-   {EndDateLong} - end date of the report document generation formatted with the **long date pattern** of the operating system.

-   {ExecutionTime} - elapsed time of the report document generation.

-   {ExecutionTimeDays} - elapsed time of the report document generation in **days**.

-   {ExecutionTimeHours} - elapsed time of the report document generation in **hours **.

-   {ExecutionTimeMinutes} - elapsed time of the report document generation in **minutes **.

-   {ExecutionTimeSeconds} - elapsed time of the report document generation in **seconds **.

-   {ExecutionTimeMilliseconds} - elapsed time of the report document generation in **milliseconds **.

