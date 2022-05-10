---
title: Report Server Manager Overview
page_title: Report Server Manager Overview
description: Overview of the common functionality for all Report Server Manager Views - Search, Sorting, etc.
slug: report-server-manager-overview
tags: search, sorting, reports, categories, users
published: True
position: 800
---

# Report Server Manager

The Report Server Manager is the ASP.NET Application that lets the Report Server users login and use its functionality through a user-friendly interface. It provides a dedicated view for each functionality of the server. These views are explained in detail in the corresponding articles:

* [Reports Management]({%slug reports-management%})

* [Categories Management]({%slug categories-management%})

* [Data Connections Management]({%slug data-connections-management%})

* [Scheduled Tasks Management]({%slug tasks-management%})

* [Data Alerts Management]({%slug alerts-management%})

* [Webhooks Management]({%slug webhooks-management%})

* [Users]({%slug users%})

* [User Roles]({%slug user-roles%}) 

The purpose of this article is to describe the common functionality of the Report Server views that would let you access and organize your Report Server assest easier. This includes [Sorting](#Sort), [Page Size](#page-size) and [Searching](#search).


## Sort

The Report Server allows you to sort the items in each view by the grid columns in _Ascending_ and _Descending_ order. The views support multi-column sorting. The order is displayed with an arrow on the right of the column name. The upward arrow indicates _Ascending_ order, the downward arrow indicates _Descending_ order. If there is no user-defined sorting, the default sorting gets applied. The next table describes the default sorting for the views:

>caption Default Sorting

| View | Primary field | Secondary field | Tertiary field |
|---|---|---|---|
|__Reports__| Favorite | Date Modified | Name |
|__Categories__| Name | | |
|__Data__| Name | | |
|__Scheduling__| Enabled | Next Occurance | Name |
|__Data Alerts__| Enabled | Last Run | Name |
|__Users__| Username | | |
|__Roles__| Name | | |
|__Webhooks__| Webhook URL | | |

The items' order in the multi-column sorting depends on the sequence in which you have applied sorting to the columns. The sorting applied earlier is prioritized. For example, if you sort the Reports view first by `Category`, and then by `Name/Description`, the grid will sort the items by `Category` and then would apply the sorting within each category by report `Name/Description` as shown in the next image. 

>caption __Sorting__ and __Page Size__ in Report Server Grid Views

![Sorting and Page Size](../../images/report-server-images/sorting-page-size.png)

If you sort first by `Name/Description`, the grid will sort the items by this column, and when you apply a secondary sorting by `Category` it would be applied to the already sorted list. This may have effect only when there are reports with the same name in different categories.

The Sorting is kept in the [browser's Window Local Storage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage). This means that the sorting is applied for each client individually. The local storage property name is `sortArray`.

## Page Size

The Page Size indicates the number of items that would be listed per page. You may choose between the values `10, 20, 50, 100`. The default is `20`. The number of the items per page and the total number of items is displayed at the bottom of the page, in the right corner of the footer (see the image above). 

You may navigate between the pages through the buttons at the left corner of the footer as shown in the image.

The Page Size is kept in the [browser's Window Local Storage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage). This means that the page size is applied for each client individually. The local storage property name is `pageSize`.

## Search

The search text box is located on top of the search supporting pages. To search for an item, specify all or part of the text that you want to match. The search starts to filter the grid after the second character. Still you can press Enter or the search button to invoke search. The characters in the grid that match the search string are highlighted. The search string is not case-sensitive. You cannot use search operators such as plus (+) or minus (–) symbols to require or exclude search criteria. The search is working with the exact input character match.
