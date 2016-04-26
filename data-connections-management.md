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



The Data Connections View is a centralized place from which you can manage the connection strings of the reports' data sources. In this way by using a named connection string you can easily change the location of the database without actually modifying the report definitions.

The data connections view provides the following functions:

  - _Search by Name, Data Provider or Connection String. For more information, see [Search]({%slug search%})_

  - _Add a data connection_

A new data connection is defined by a _name_, a _description_, a _data provider_ and a _connection string_.
>Make sure the connection string is referencing SQL server with a non local address, so the users can edit reports in the report designer. To have access to read/write/modify connection strings, including from the Standalone Report Designer, the user must have permissions for the Data Connections View or the user must be in the corresponding role - see [User Roles](/user-management/user-roles.md). Without write permissions for the Data Connections View, the user will be able to publish a report with connection strings hard-coded in the definition.

Data connections with duplicate names are not allowed.

  - _Edit a data connection_  
The properties of an existing data connection can be modified at any time.
  - _Delete a data connection_  
You can delete an existing data connection when it is not used any more.
  - _Copy a data connection_  
To create a similar to an existing connection you can simply copy the source connection and modify its properties.
