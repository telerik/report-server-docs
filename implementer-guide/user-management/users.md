---
title: Users and Permissions
page_title: Users and Permissions
description: Users and Permissions
slug: users
tags: users
published: True
position: 200
---

# Users and Permissions

## Manage Users

### Register New User

Each user is registered with the following information:

-   *Authentication Provider* - in case you have set up an external authentication provider (AD FS), a **Federation** entry will be added in the drop-down list. Otherwise only **Local** is available.

-   *Username*

-   *Password* - available only for local accounts. By default the password must conform to the following rules:

    -   at least 6 characters long
        
    > If a mail (SMTP) server is configured there is no need to specify a password for the new local user. After saving the new user a mail with a special activation link will be send to the user's e-mail address. When clicking on the link the user will be taken to a page to set his/her password and after doing so he/she will be redirected to the login page.

-   *Email*

-   *First Name* - available only for local accounts. When creating a Federation user, its names will be populated upon first login using AD FS.

-   *Last Name* - available only for local accounts.

-   *Roles* - optional. You can assign the user to one or more existing user roles.

### Modify User

You can change the following user settings:

-   *Email*

-   *First Name*

-   *Last Name*
    
-   *Password*
    
-   *Enabled*

Users cannot be deleted. In order to stop the access for a user and free a CAL the user should be disabled.

### Manage User Permissions

You can add/remove permissions by clicking on the Manage Permissions button from the Permissions tab.

## Manage Permissions

You can grant permissions to a user from the **Apply Roles** and **Add Permission** tabs.

The Apply Roles tab allows assigning users to user roles. The user can simultaneously belong to more than one user group. In this way he/she receives the permissions of the user role.

The Add Permission tab allows giving specific permissions to users. Each permission has an **Access Mode**, **Scope**, and **Target**:

### Access Modes

-   *Read* - gives a **read** permission for the selected scope.

-   *Modify* - gives an **edit** permission for the selected scope.

-   *Delete* - gives **delete** permission for the selected scope.

-   *Create* - gives **create** permission for the selected scope.

> *Modify* and *Delete* access modes require *Read* access. *Create* access mode **cannot** have a specific scope (e.g. *Specific Report*, *Specific Category*, *Specific Data Connection*).

### Scopes

-   *All Reports* - the permission applies to all the reports.

-   *Reports in Category* - the permission applies to all the reports that belong to a specific category.

-   *Specific Report* - the permission applies to a specific report.

-   *All Categories* - the permission applies to all categories.

-   *Specific Category* - the permission applies to a specific category.

-   *All Data Connections* - the permission applies to all data connections.

-   *Specific Data Connection* - the permission applies to a specific data connection.

-   *All Tasks* - the permission applies to all tasks.

-   *Specific Task* - the permission applies to a specific task.

### Targets

The scope target depends on the selected scope:

-   For *Reports in Category* scope you have to choose a specific *Category*.

-   For *Specific Report* scope you have to choose a specific *Report*.

-   For *Specific Category* scope you have to choose a specific *Category*.

-   For *Specific Data Connection* scope you have to choose a specific *Data Connection*.

-   For *Specific Task* scope you have to choose a specific *Task*.
