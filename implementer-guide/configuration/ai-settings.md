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

During the report preview phase, AI-generated insights offer an extensive suite of functionalities, including the formulation of responses, the construction of prompts, engagement with AI-generated content, and the execution of predefined instructions.

![An image of the Report Server with the AI Dialog being opened](images/AIPromptReportServer.png)

## AI Integration

The AI settings view allows you to configure exactly how you want to use our AI feature and its options through the user interface. By default, the `Enable AI` checkbox is set to false, which disables the entire page. You will still be able to copy any content you need, but dropdown selections and checkbox changes will be unavailable.

> If `Enable AI` is set to false and the Kendo AI prompt is not present in the report viewers, the AI configuration section will not be displayed in the Report Server.

If `Enable AI` is set to true, you will be able to configure the AI by following these steps:

1. Choose one of the following providers:

![An image of the providers supported by the Report Server ](images/AIProvidersReportServer.png)

1. Select a `Model Name`, specify the `Server Endpoint` and the `API Key`

![An image of the Model Name, Server Endpoint, and API Key fields](images/modelNameServiceEndpointAPIKey.png)

1. If all fields are filled in, you can test the integration using the `Test Integration` button. This will ping the selected provider with the specified information and send a request using a test prompt. If everything is configured correctly, you will receive a response saying `Integration successful`. If there is a problem, a pop-up will appear with detailed error information.

![An image of the of the message that will appear if the fields are filled in correctly.](images/testIntegrationSuccessfulMessage.png)

![An image of the message that will appear if the fields are filled in incorrectly.](images/testIntegrationFailedMessage.png)

## AI-Powered Report Document Insights

From this panel, you can choose whether to display a content message by setting the `Show content message` checkbox to true.

![An image of the Content Message](images/showConsentMessageButton.png)

> If `Show content message` is set to true and the content message field is empty, you will not be able to save the changes.

### Prompts Settings

You can create as many Predefined Prompts as needed. You can also delete any prompts that are no longer required. However, if there is only one Predefined Prompt, it cannot be deleted.

![Image of the Predefined Prompts in the Report Server](images/PredefinedPromptsReportServer.png)

The `Allow custom prompts` checkbox enables or disables the ability for end users to send custom requests to the AI.

![Image of the 'Allow custom prompts' checkbox](images/AllowCustomPromptsButton.png)

If all settings have been configured correctly and the changes have been saved, the following message will appear on the screen.

![Image of the message 'The new settings have been saved successfully' in the Report Server Configuration](images/SavedSuccessfullyMessage.png)

### Consent

Before any user can use this feature, upon opening the AI Prompt Dialog, they will be asked to give consent to the AI to process the provided text.

![An Image of how the AI Prompt Consent Dialog Appears in the Report Server](images/ConsentMessage.png)

### Ask AI Prompt

After consent is given, the prompt for asking the AI questions will appear in the top-right corner of the report viewer. The UI will change depending on whether custom questions are allowed.

![An Image of how the Ask AI Prompt will look with custom questions in the Report Server](images/AskAIPromptReportServer.png)

### Output

The Output of the AI processor will be displayed in the Output tab of the Ask AI Prompt after the result has been generated:

![An Image of how the Ask AI Prompt will look when the output has been generated in the Report Server](images/OutputPromptReportServer.png)
