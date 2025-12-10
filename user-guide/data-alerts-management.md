---
title: Data Alerts Management
page_title: Managing Telerik Report Server's Data Alerts
description: "Understand how to create, modify, and delete Telerik Report Server data alerts. Learn more about the available configuration options, such as report target formats, mail templates, and data alert scheduling."
slug: alerts-management
tags: scheduling,alerts,management
published: True
position: 710
---

# Data Alerts Management

The `Data Alerts` view is the place from where you can manage data alerts, review the alerts' execution, and manage subscribers.

## Data Alerts Grid

The `Data Alerts` grid allows you to create, modify, and delete data alerts.

- A Data Alert runs at a scheduled time and checks whether specific data conditions are satisfied. If the data conditions are satisfied a report document or a collection of report documents are generated and sent to the alert's subscribers.
- A data alert can be run only once or on a recurrent basis, for example: daily, weekly, monthly or yearly. Within the recurrence rule, you set the intervals and range for how often a data alert is to be run.
- A Data Alert has various settings which are grouped into different tabs.

### General Tab

- `Enabled` - specifies whether the data alert is enabled or not.
- `Name` - the name of the data alert. It should be unique among the other data alerts.
- `Start` - the actual start date of the data alert.
- `Repeat` - defines the recurrence rule if the data alert should be executed at regular intervals. The repeat pattern can be daily, weekly, monthly, or yearly. Currently, hourly repetition is not supported.

### Reports Tab

The Reports tab allows you to define a collection of reports for the `Data Alerts`. Each report has to have the following settings.

- A `Report` from a selected `Category`.
- Target `Document format` - can be any single document format provided by the Telerik Reporting engine:

  - PDF - renders a report in the Adobe Acrobat Reader. The format is shown as an Acrobat (PDF) File in the Export drop-down of the report toolbar.
  - XLS - renders a report in Microsoft Excel. The report opens in Microsoft Excel 97 or later.
  - CSV - renders a report in comma-delimited format. The report opens in a viewing tool associated with CSV file formats.
  - RTF - renders a report in Rich Text Format. The report opens in Microsoft Word 97 or later.
  - XPS - renders a report in XML Paper Specification (XPS) format - electronic representation of digital documents based on XML. The report opens in Microsoft XPS Viewer.
  - DOCX - renders a report in Microsoft Word 2007 format (also known as OpenXML) - it is a zipped, XML-based file format developed by Microsoft for representing word processing documents.
  - XLSX - renders a report in Microsoft Excel 2007 format (also known as OpenXML) - it is a zipped, XML-based file format developed by Microsoft for representing spreadsheets.
  - PPTX - renders a report in Microsoft PowerPoint 2007 format (also known as OpenXML) - it is a zipped, XML-based file format developed by Microsoft for presentations.
  - MHTML - renders a report in MHTML. The report opens in Internet Explorer. The format is shown as Web Archive in the Export drop-down of the report toolbar.

- A `Parameters` - the parameter values that will be used for the report when the data alert is executed. The parameters area includes all report parameters of the report regardless of their visibility (visible or invisible).

  By default, the invisible report parameters will use their values specified at design time, i.e. they are not overridden by the parameter values specified in the parameters. If you want to override the invisible parameters' values with the alert's parameters you have to uncheck the "_Use Default Value_" checkbox.

  The "_Use Default Value_" checkbox for all parameters determines whether the value of the report parameter specified at design time will be used or whether it will be overridden by the value that you have specified in the alert's parameters. When it is checked the design time value of the report parameter will be used and when it is unchecked the stored in the alert parameters value will be used.

### Rules Tab

The rules are used to define conditions that report data should satisfy in order for the alert to be triggered. Rules are set on exactly one DataItem in one Report.

First, select a Report from available reports coming from the Reports tab, then a DataItem from it. After choosing a Report and DataItem, in the Rules grid define the actual rules for the data that the item displays.

When defining a rule, the Expression part should contain the name of a TextBox item that holds a dynamic expression. During the alert processing, its value will be compared to the value in the Value part of the rule.

The supported comparisons are `is`, `is not`, `is greater than`, `is greater than or equal to`, `is less than`, `is less than or equal to`, `in`, `like`, `not like`. Currently, data alerts can be defined only on a Table(Crosstab) item.

### Mail Template (Local) Tab

Specifies the mail template which is sent to the added local users for the alert, when the data conditions are met and the report document has been successfully generated.

When there is an error during the report processing or a general error during the data alert execution then the **Configuration** | **Mail Templates** | **Data Alert Error** mail template is used.

Data alert error emails will be sent to the **System Administrator** and **Report Creator** [roles]({%slug user-roles%}) only.

If you haven't explicitly changed this template then the template from **Configuration** | **Mail Templates** | **Data Alert Attachment** will be used.

In the template, you can use the following mail variables which will be replaced automatically when the alert is executed:

- `{FirstName}` - the first name of the user.
- `{LastName}` - the last name of the user.
- `{AlertName}` - the name of the data alert.
- `{StartTime}` - start time of the report document generation.
- `{StartTimeShort}` - start time of the report document generation formatted with the **short time pattern** of the operating system.
- `{StartTimeLong}` - start time of the report document generation formatted with the **long time pattern** of the operating system.
- `{StartDate}` - start date of the report document generation formatted with the **short date pattern** of the operating system.
- `{StartDateLong}` - start date of the report document generation formatted with the **long date pattern** of the operating system.
- `{EndTime}` - end time of the report document generation.
- `{EndTimeShort}` - end time of the report document generation formatted with the **short time pattern** of the operating system.
- `{EndTimeLong}` - end time of the report document generation formatted with the **long time pattern** of the operating system.
- `{EndDate}` - end date of the report document generation formatted with the **short date pattern** of the operating system.
- `{EndDateLong}` - end date of the report document generation formatted with the **long date pattern** of the operating system.
- `{ExecutionTime}` - elapsed time for the report document generation.
- `{ExecutionTimeDays}` - elapsed time for the report document generation in **days**.
- `{ExecutionTimeHours}` - elapsed time for the report document generation in **hours**.
- `{ExecutionTimeMinutes}` - elapsed time for the report document generation in **minutes**.
- `{ExecutionTimeSeconds}` - elapsed time for the report document generation in **seconds**.
- `{ExecutionTimeMilliseconds}` - elapsed time for the report document generation in **milliseconds**.
- `{ReportName}` - the name of the report document.
- `{DocumentFormat}` - the specified in the report rendering format.
- `{Link}` - the link of the generated report.
- `{@[ReportParameter.Name]}` - the values of the specified by the `[ReportParameter.Name]` all reports parameters used when running the scheduling task. The `[ReportParameter.Name]` placeholder stands for the actual name of the report parameters. The list of all possible report parameters that can be used in the mail template is available through the _variables_ dropdown in the Kendo editor.

### Mail Template (External) Tab

Specifies the mail template which is sent to the added external users for the alert, when the data conditions are met and the report(s) document has been successfully generated.

When there is an error during the report processing or a general error during the data alert execution then the **Configuration** | **Mail Templates** | **Data Alert Error** mail template is used. Data alert error emails will be sent to the **System Administrator** and **Report Creator** [roles]({%slug user-roles%}) only.

If you haven't explicitly changed this template then the template from **Configuration** | **Mail Templates** | **Data Alert Attachment** will be used.

In the template, you can use the following mail variables which will be replaced automatically when the alert is executed:

- `{AlertName}` - the name of the data alert.
- `{StartTime}` - start time of the report document generation.
- `{StartTimeShort}` - start time of the report document generation formatted with the **short time pattern** of the operating system.
- `{StartTimeLong}` - start time of the report document generation formatted with the **long time pattern** of the operating system.
- `{StartDate}` - start date of the report document generation formatted with the **short date pattern** of the operating system.
- `{StartDateLong}` - start date of the report document generation formatted with the **long date pattern** of the operating system.
- `{EndTime}` - end time of the report document generation.
- `{EndTimeShort}` - end time of the report document generation formatted with the **short time pattern** of the operating system.
- `{EndTimeLong}` - end time of the report document generation formatted with the **long time pattern** of the operating system.
- `{EndDate}` - end date of the report document generation formatted with the **short date pattern** of the operating system.
- `{EndDateLong}` - end date of the report document generation formatted with the **long date pattern** of the operating system.
- `{ExecutionTime}` - elapsed time for the report document generation.
- `{ExecutionTimeDays}` - elapsed time for the report document generation in **days**.
- `{ExecutionTimeHours}` - elapsed time for the report document generation in **hours**.
- `{ExecutionTimeMinutes}` - elapsed time for the report document generation in **minutes**.
- `{ExecutionTimeSeconds}` - elapsed time for the report document generation in **seconds**.
- `{ExecutionTimeMilliseconds}` - elapsed time for the report document generation in **milliseconds**.
- `{ReportName}` - the name of the report document.
- `{DocumentFormat}` - the specified in the report rendering format.
- `{Link}` - the link of the generated report.
- `{@[ReportParameter.Name]}` - the values of the specified by the `[ReportParameter.Name]` all reports parameters used when running the scheduling task. The `[ReportParameter.Name]` placeholder stands for the actual name of the report parameters. The list of all possible report parameters that can be used in the mail template is available through the _variables_ dropdown in the Kendo editor.

## Activity View

The `Activity` view for a data alert shows the alert execution history. Created documents from each execution, can be downloaded for preview in the target format.

An execution item can be deleted, which will trigger deleting for all generated documents from this specific execution.

## Subscribers View

From the `Subscribers` view, you can manage who will receive the created documents as mail attachments. A subscriber can be an existing report server user or an external user who is represented through an e-mail address.

The emails should be separated with a new line, a semicolon `;` or a comma `,`.

> When there is an error during the report processing or a general error in the data alert execution, emails will be sent to the **System Administrator** and **Report Creator** [roles]({%slug user-roles%}) only.

## Telerik Report Server Learning Resources

- [Telerik Report Server Homepage](https://www.telerik.com/report-server)
- [Telerik Report Server Installation]({%slug installation%})
- [Telerik Report Server User Management]({%slug user-management%})
- [Connecting to Data with Telerik Report Server]({%slug connecting-to-data%})
- [Telerik Report Server License Agreement](https://www.telerik.com/purchase/license-agreement/report-server)
