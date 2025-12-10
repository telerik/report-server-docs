---
title: Data Connections Management
page_title: Data Connections Management
description: Data Connections Management
slug: data-connections-management
tags: data,connections,management
published: True
position: 600
---

# Data Connections Management

The Data Connections View is a centralized place from which you can manage the connection strings of the reports' [SQL data sources](https://docs.telerik.com/reporting/sqldatasource).

In this way, by using a named connection string, you can easily change the location of the database without actually modifying the report definitions. The view also displays read-only Business Object data connections which you can use inside a report.

> tip For more information on using business objects as report data sources refer to [Business Objects Management]({%slug business-objects-management%}).

The Data Connections View provides the following functions:

- _Add a data connection_ - a new data connection is defined by a _name_, a _description_, a _data provider_ and a _connection string_

  > Data connections with duplicate names are not allowed.

- _Edit a data connection_ - the properties of an existing data connection can be modified at any time
- _Delete a data connection_ - you can delete an existing data connection when it is not used anymore
- _Copy a data connection_ - to create a similar to an existing connection you can simply copy the source connection and modify its properties
- _Search_ by Name, Data Provider, or Connection String. For more information, see [Search]({%slug search%}#search)

> In order to read, write, or modify connection strings from the Report Server or from the Standalone Report Designer, the user must have permission for the Data Connections View or they must be assigned the corresponding role - see [User Roles]({%slug user-roles%}).

## Telerik Report Server Learning Resources

- [Telerik Report Server Homepage](https://www.telerik.com/report-server)
- [Telerik Report Server Installation]({%slug installation%})
- [Telerik Report Server User Management]({%slug user-management%})
- [Connecting to Data with Telerik Report Server]({%slug connecting-to-data%})
- [Telerik Report Server License Agreement](https://www.telerik.com/purchase/license-agreement/report-server)
