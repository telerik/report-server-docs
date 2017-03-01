---
title: Users
page_title: Users
description: Users
slug: users
tags: users
published: True
position: 200
---

# Users



You can perform the following actions from the *Users* view:

-   **Register new user** - each user is registered with the following information:

    -   *Authentication provider* - in case you have set up an external authentication provider (AD FS), a **Federation** entry will be added in the drop-down list. Otherwise only **Local** is available.

    -   *Username*

    -   *Password* - available only for local accounts. By default the password must conform to the following rules:

        -   at least 6 characters long
        
        If a mail (SMTP) server is configured there is no need to specify a password for the new local user. After saving the new user a mail with a special activation link will be send to the user's e-mail address. When clicking on the link the user will be taken to a page to set his/her password and after doing so he/she will be redirected to the login page.

    -   *Email*

    -   *First name* - available only for local accounts. When creating a Federation user, its names will be populated upon first login using AD FS.

    -   *Last Name* - available only for local accounts

    -   *Roles* - optional. You can assign the user to one or more existing user roles.

-   **Modify user** - you can change the following user settings:

    -   *Email*

    -   *First name*

    -   *Last name*
    
    -   *Password*
    
    -   *Enabled*

-   **Manage permissions** - You can add/remove permissions by clicking on the MANAGE PERMISSIONS button from the PERMISSIONS tab.

You can grant permissions to a user in two ways:

-   **APPLY ROLES** tab - by assigning the user to user roles. The user can simultaneously belong to more than one user group. In this way he/she receives the permissions of the user role.

-   **ADD PERMISSION** tab - by giving individual permissions. Each permission has the following structure:

    -   **Access mode**:

        -   *Read* - gives a **read** permission for the selected scope

        -   *Modify* - gives an **edit** permission for the selected scope

        -   *Delete* - gives **delete** permission for the selected scope

        -   *Create* - gives **create** permission for the selected scope

*Modify* and *Delete* access modes require *Read* access. *Create* access mode **cannot** have a specific scope (e.g. *Specific Report*, *Specific Category*, *Specific Data Connection*).

-   **Scope:**

    -   *All Reports* - the permission applies to all the reports

    -   *Reports in Category* - the permission applies to all the reports that belong to a specific category

    -   *Specific Report* - the permission applies to a specific report

    -   *All Categories* - the permission applies to all categories

    -   *Specific Category* - the permission applies to a specific category

    -   *All Data Connections* - the permission applies to all data connections

    -   *Specific Data Connection* - the permission applies to a specific data connection

    -   *All Tasks* - the permission applies to all tasks

    -   *Specific Task* - the permission applies to a specific task

-   **Target**

The scope target depends on the selected scope:

-   For *Reports in Category* scope you have to choose a specific *Category*.

-   For *Specific Report* scope you have to choose a specific *Report*.

-   For *Specific Category* scope you have to choose a specific *Category*.

-   For *Specific Data Connection* scope you have to choose a specific *Data Connection*.

-   For *Specific Task* scope you have to choose a specific *Task*.
