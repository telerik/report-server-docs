---
title: Telerik Report Server Accessibility
page_title: Telerik Report Server Accessibility
description: Telerik Report Server Accessibility
slug: accessibility
tags: Telerik Report Server, Accessibility
published: True
position: 801
---

# Telerik Report Server Accessibility

The most powerful technology in the world is technology that everyone, including people with disabilities, can use.
Progress® Telerik® Report Server aims to provide the best access to its features for everyone who is using it.  

Progress® Telerik® Report Server uses Progress Kendo UI framework for UI representation.
More additional information, about keyboard support within kendo widgets, can be found in the
[Kendo UI for jQuery Documentation](https://docs.telerik.com/kendo-ui/accessibility/keyboard-support#built-in-support).

## Supported accessibility features

Progress® Telerik® Report Server support the following important accessibility features:


### Comprehensive keyboard support

Includes navigation between and into Report Server areas (menus, contents, detail or search sections) using shortcut keys,
TAB or arrow keys where possible.

The default shortcut keys for navigation between the Report Server areas are:

*	`Ctrl` + `Alt` + `h` - opens accessibility window with all keyboard shortcuts
*	`Ctrl` + `Alt` + `a` - top banner bar area
*	`Ctrl` + `Alt` + `m` - side navigation
*	`Ctrl` + `Alt` + `c` - page content
*	`Ctrl` + `Alt` + `l` - list of items (reports, categories, users, etc)
*	`Ctrl` + `Alt` + `s` - search field
*	`Ctrl` + `Alt` + `d` - detail section on the right of the list of items 
*	`Ctrl` + `Alt` + `t` – tab items within modal window 


### Dynamically generated descriptions for Report Server areas

The report server areas provide additional textual details that reflect to the user interaction - 
for example when a new item from the list is selected or when a report is added or removed from the user favorite collection.
Progress® Telerik® Report Server uses Kendo MVVM design pattern to set dynamically changed aria-labels. 
For further information check the [Kendo UI for jQuery Documentation](https://docs.telerik.com/kendo-ui/framework/mvvm/overview).
