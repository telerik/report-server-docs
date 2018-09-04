---
title: Scheduled Tasks Management
page_title: Scheduled Tasks Management
description: Scheduled Tasks Management
slug: tasks-management
tags: scheduling,tasks,management
published: True
position: 700
---

# Scheduled Tasks Management

The **Scheduling** view is a centralized place from which you can manage scheduled tasks, review the created by the tasks documents and manage subscribers.

## Scheduling Grid

The **Scheduling** grid allows you to create, modify and delete scheduled tasks. A scheduled task specifies when a collection of reports should be rendered and in what document formats. The created documents are stored in the Report Server's storage and can be sent as email attachments to different subscribers. A scheduled task can be run only once or on a recurrent basis, for example: daily, weekly, monthly or yearly. Within the recurrence rule, you set the intervals and range for how often a report execution is to occur.

A Scheduled Task has various settings which are grouped into different tabs. 

### General Tab

-   **Enabled** - the task can be temporary disabled without the need to delete it.

-   **Name** - the name of the task. It should be unique among the tasks.

-   **Start** - the actual start date of the task.

-   **Repeat** - defines the recurrence rule if the task should be executed on regular intervals. The repeat pattern can be daily, weekly, monthly and yearly. Currently, hourly repetition is not supported.

### Reports Tab

The reports tab allow you to define the collection of reports for the task. Each report has to have the following settings.

-   A **Report** from a selected **Category**.

-   Target **Document format** - can be any single document format provided by the Telerik Reporting engine:

    -   PDF - renders a report in the Adobe Acrobat Reader. The format is shown as Acrobat (PDF) File in the Export drop-down of the report toolbar.

    -   XLS - renders a report in Microsoft Excel. The report opens in Microsoft Excel 97 or later.

    -   CSV - renders a report in comma-delimited format. The report opens in a viewing tool associated with CSV file formats.

    -   RTF - renders a report in Rich Text Format. The report opens in Microsoft Word 97 or later.

    -   XPS - renders a report in XML Paper Specification (XPS) format - electronic representation of digital documents based on XML. The report opens in Microsoft XPS Viewer.

    -   DOCX - renders a report in Microsoft Word 2007 format (also known as OpenXML) - it is a zipped, XML-based file format developed by Microsoft for representing word processing documents.

    -   XLSX - renders a report in Microsoft Excel 2007 format (also known as OpenXML) - it is a zipped, XML-based file format developed by Microsoft for representing spreadsheets.

    -   PPTX - renders a report in Microsoft PowerPoint 2007 format (also known as OpenXML) - it is a zipped, XML-based file format developed by Microsoft for presentations.

    -   MHTML - renders a report in MHTML. The report opens in Internet Explorer. The format is shown as Web Archive in the Export drop-down of the report toolbar.

-   A **Parameters** - the parameter values that will be used for the report when the task is executed. The parameters area includes all report parameters of the report regardless their visibility (visible or invisible). By default the invisible report parameters will use their values specified at design time, i.e. they are not overridden by the parameter values specified in the task. If you want to override the invisible parameters' values with the task's parameters you have to uncheck the "*Use Default Value*" checkbox.
The "*Use Default Value*" checkbox for all parameters determines whether the value of the report parameter specified at design time will be used or whether it will be overridden by the value that you have specified in the task's parameters. When it is checked the design time value of the report parameter will be used and when it is unchecked the stored in the task parameters value will be used.

### Mail Template (Local) Tab

Specifies the mail template which is sent to the added local users for the task, by the scheduling service when the report document has been successfully generated. When there is an error during the report processing or a general error in the task execution then the **Configuration** | **Mail Templates** | **Scheduled Task Error** mail template is used. Scheduled task error mails will be sent to the **System Administrator** and **Report Creator** [roles]({%slug user-roles%}) only.
If you haven't explicitly changed this template then the template from **Configuration** | **Mail Templates** | **Scheduled Task Attachment** will be used.
In the template you can use the following mail variables which will be replaced automatically when the task is executed:

-   {FirstName} - the first name of the user.

-   {LastName} - the last name of the user.

-   {TaskName} - the name of the scheduled task.

-   {StartTime} - start time of the report document generation.

-   {StartTimeShort} - start time of the report document generation formatted with the **short time pattern** of the operating system.

-   {StartTimeLong} - start time of the report document generation formatted with the **long time pattern** of the operating system.

-   {StartDate} - start date of the report document generation formatted with the **short date pattern** of the operating system.

-   {StartDateLong} - start date of the report document generation formatted with the **long date pattern** of the operating system.

-   {EndTime} - end time of the report document generation.

-   {EndTimeShort} - end time of the report document generation formatted with the **short time pattern** of the operating system.

-   {EndTimeLong} - end time of the report document generation formatted with the **long time pattern** of the operating system.

-   {EndDate} - end date of the report document generation formatted with the **short date pattern** of the operating system.

-   {EndDateLong} - end date of the report document generation formatted with the **long date pattern** of the operating system.

-   {ExecutionTime} - elapsed time for the report document generation.

-   {ExecutionTimeDays} - elapsed time for the report document generation in **days**.

-   {ExecutionTimeHours} - elapsed time for the report document generation in **hours**.

-   {ExecutionTimeMinutes} - elapsed time for the report document generation in **minutes**.

-   {ExecutionTimeSeconds} - elapsed time for the report document generation in **seconds**.

-   {ExecutionTimeMilliseconds} - elapsed time for the report document generation in **milliseconds**.

-   {ReportName} - the name of the report.

-   {DocumentFormat} - the specified in the report rendering format.

-   {Link} - the link of the generated report.

-   {@\[ReportParameter.Name\]} - the values of the specified by the \[ReportParameter.Name\] reports parameters used when running the scheduling task. The \[ReportParameter.Name\] placeholder stands for the actual name of the reports parameters. The list of all possible reports parameters that can be used in the mail template is available through the *variables* dropdown in the Kendo editor.


### Mail Template (External) Tab

Specifies the mail template which is sent to the added external users for the task, by the scheduling service when the report document has been successfully generated. When there is an error during the report processing or a general error in the task execution then the **Configuration** | **Mail Templates** | **Scheduled Task Error** mail template is used. Scheduled task error mails will be sent to the **System Administrator** and **Report Creator** [roles]({%slug user-roles%}) only.
If you haven't explicitly changed this template then the template from **Configuration** | **Mail Templates** | **Scheduled Task Attachment** will be used.
In the template you can use the following mail variables which will be replaced automatically when the task is executed:

-   {TaskName} - the name of the scheduled task.

-   {StartTime} - start time of the report document generation.

-   {StartTimeShort} - start time of the report document generation formatted with the **short time pattern** of the operating system.

-   {StartTimeLong} - start time of the report document generation formatted with the **long time pattern** of the operating system.

-   {StartDate} - start date of the report document generation formatted with the **short date pattern** of the operating system.

-   {StartDateLong} - start date of the report document generation formatted with the **long date pattern** of the operating system.

-   {EndTime} - end time of the report document generation.

-   {EndTimeShort} - end time of the report document generation formatted with the **short time pattern** of the operating system.

-   {EndTimeLong} - end time of the report document generation formatted with the **long time pattern** of the operating system.

-   {EndDate} - end date of the report document generation formatted with the **short date pattern** of the operating system.

-   {EndDateLong} - end date of the report document generation formatted with the **long date pattern** of the operating system.

-   {ExecutionTime} - elapsed time for the report document generation.

-   {ExecutionTimeDays} - elapsed time for the report document generation in **days**.

-   {ExecutionTimeHours} - elapsed time for the report document generation in **hours**.

-   {ExecutionTimeMinutes} - elapsed time for the report document generation in **minutes**.

-   {ExecutionTimeSeconds} - elapsed time for the report document generation in **seconds**.

-   {ExecutionTimeMilliseconds} - elapsed time for the report document generation in **milliseconds**.

-   {ReportName} - the name of the report.

-   {DocumentFormat} - the specified in the report rendering format.

-   {Link} - the link of the generated report.

-   {@\[ReportParameter.Name\]} - the values of the specified by the \[ReportParameter.Name\] reports parameters used when running the scheduling task. The \[ReportParameter.Name\] placeholder stands for the actual name of the reports parameters. The list of all possible reports parameters that can be used in the mail template is available through the *variables* dropdown in the Kendo editor.

> A new task can be also created directly from the **Reports** | **Scheduling** view.

You can search for tasks by their Name, Report, or Document Format. For more information, see [Search]({%slug search%}).

## Activity View

The **Activity** view for a scheduled task shows the task execution history. Created documents from each execution, can be downloaded for preview in the target format. An execution item can be delete, which will trigger deleting for all generated documents from this specific execution.

## Subscribers View

From the **Subscribers** view, you can manage who will receive the created documents as mail attachments. A subscriber can be an existing report server user or an external user which is represented through his email. The external emails should be separated with semicolon (;) or comma (,).

> When there is an error during the report processing or a general error in the task execution, mails will be sent to the **System Administrator** and **Report Creator** [roles]({%slug user-roles%}) only.
