---
title: Webhooks
page_title: Webhooks
description: Webhooks Settings
slug: webhooks
tags: Webhooks,settings
published: True
position: 700
---

# Webhooks

Starting with [Report Server 2026 Q4 (12.3.26.1110)](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-2026-q4-(12-3-26-1110)), Report Server takes the Report Server base URL from the **Server URL** on the **Security** tab.

The **Report Server base URL** tells Report Server which address to use to send webhook notifications to itself. To use a different URL, set it on **Configuration > Webhooks**.

Enter an absolute HTTP or HTTPS URL for this Report Server, such as `http://localhost/`. Leave the field empty to disable webhook notifications.

>important When you save a changed main Server URL, Report Server replaces the Report Server base URL with it. If a custom Webhooks URL differs from the main URL, re-enter it on the **Webhooks** tab after you change the main URL.

>note In versions earlier than 12.3.26.1110, the Report Server base URL was automatically retrieved and stored on the first start of the Report Server management application. If the address later changed because of an environment change, you had to update the base URL manually.

## See Also

The following articles provide more information:

- [Security settings]({%slug security%})
- [Webhooks Management]({%slug webhooks-management%})
