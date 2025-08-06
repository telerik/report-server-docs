---
title: AI 
page_title: AI
description: AI Settings
slug: designer
tags: AI,settings
published: True
position: 50
---

# AI Overview

Beginning with the 2025 Q3 release, we are introducing the new AI Settings to our Report Server. The AI configuration includes two panels — __AI Integration__ and __AI-Powered Report Document Insights__.

## AI Integration

The AI settings view allows you to configure exactly how you want to use our AI feature and its options through the user interface. By default, the `Enable AI` checkbox is set to false, which disables the entire page. You will still be able to copy any content you need, but dropdown selections and checkbox changes will be unavailable.

> If `Enable AI` is set to false and the Kendo AI prompt is not present in the report viewers, the AI configuration section will not be displayed in the Report Server.

If `Enable AI` is set to true, you will be able to configure the AI by following these steps:

1. Choose one of the following providers:

![](images/)

1. Select a `Model Name` and specify the `Server Endpoint`

![](images/)

1. If all fields are filled in, you can test the integration using the `Test Integration` button. This will ping the selected provider with the specified information and send a request using a test prompt. If everything is configured correctly, you will receive a response saying `Integration successful`. If there is a problem, a pop-up will appear with detailed error information.

![](images/)

![](images/)

## AI-Powered Report Document Insights

From this panel, you can choose whether to display a content message by setting the `Show content message` checkbox to true.

![](images/)

> If `Show content message` is set to true and the content message field is empty, you will not be able to save the changes.

### Predefined Prompts

You can create as many Predefined Prompts as needed. You can also delete any prompts that are no longer required. However, if there is only one Predefined Prompt, it cannot be deleted.

The `Allow custom prompts` checkbox enables or disables the ability for end users to send custom requests to the AI.

![](images/)
