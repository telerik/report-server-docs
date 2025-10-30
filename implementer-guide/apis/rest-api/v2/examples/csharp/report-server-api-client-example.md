---
title: Report Server API Client
page_title: Report Server API Client Examples
description: Report Server API Client for .NET Examples
slug: report-server-api-client-examples
tags: rest, api, client, net, examples
published: True
position: 100
---

# Report Server API Client Examples

## Login

```C#
    var settings = new Settings()
    {
        BaseAddress = "https://myreportserver:83"
    };

    using (var rsClient = new ReportServerClient(settings))
    {
        rsClient.Login("username", "password");
    }
```

## Get Resource

```C#
    var category = rsClient.GetCategory("categoryId");
```

## Create Resource

```C#
    var categoryData = new CreateCategoryData()
    {
        Name = "New Category",
    };
    var newCategory = rsClient.CreateCategory(categoryData);
```

## Update Resource

```C#
    var category = rsClient.GetCategory("categoryId");
    category.Name = "Updated Name";
    var updatedCategory = rsClient.UpdateCategory(category);
```

## Delete Resource

```C#
    rsClient.DeleteCategory("categoryId");
```
