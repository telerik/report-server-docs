---
title: Accessibility
page_title: Accessibility
description: Accessibility
slug: accessibility
tags: accessibility
published: True
position: 801
---

# Accessibility

The most powerful technology in the world is technology that everyone, including people with disabilities, can use.
Report Server aims to provide the best access to its features for everyone who is using it.  

Report Server uses Progress Kendo UI framework for UI representation.
More information about keyboard support within kendo widgets can be found in the
[Kendo UI for jQuery Documentation](https://docs.telerik.com/kendo-ui/accessibility/keyboard-support#built-in-support).

## Supported Features

The following accessibility features are supported:

### Comprehensive Keyboard Support

Includes navigation between and into Report Server areas (menus, contents, detail, or search sections) using shortcut keys,
TAB, or arrow keys where possible.

The default shortcut keys for navigation between the Report Server areas are:

*	`Ctrl` + `Alt` + `H` - opens accessibility window with all keyboard shortcuts
*	`Ctrl` + `Alt` + `A` - top banner bar area
*	`Ctrl` + `Alt` + `M` - side navigation
*	`Ctrl` + `Alt` + `C` - page content
*	`Ctrl` + `Alt` + `L` - list of items (reports, categories, users, etc)
*	`Ctrl` + `Alt` + `S` - search field
*	`Ctrl` + `Alt` + `D` - detail section on the right of the list of items 
*	`Ctrl` + `Alt` + `T` – tab items within modal window 

### Dynamically Generated Descriptions for Report Server Areas

The Report Server areas provide additional textual details that reflect to the user interaction - 
for example when a new item from the list is selected or when a report is added or removed from the user favorite collection.
Report Server uses Kendo MVVM design pattern to set dynamically changed aria-labels. 
For further information check the [Kendo UI for jQuery Documentation](https://docs.telerik.com/kendo-ui/framework/mvvm/overview).
