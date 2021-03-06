---
title: Create a function in Azure triggered by a GitHub webhook | Microsoft Docs
description: Use Azure Functions to create a serverless function that is invoked by a GitHub webhook.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''

ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: glenga

---
# Create a function triggered by a GitHub webhook

Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload. 

![Github Webhook triggered function in the Azure portal](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

It should take you less than five minutes to complete all the steps in this topic.

## Prerequisites 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

You also need a GitHub account with at least one project. You can [sign up for a free GitHub account](https://github.com/join), if you don't already have one.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)] 

## <a name="create-function"></a>Create a GitHub webhook triggered function

1. Expand your function app, click the **+** button next to **Functions**, click the **GitHubWebHook** template for your desired language. **Name your function**, then click **Create**. 

2. In your new function, click **</> Get function URL**, then copy and save the values. Do the same thing for **</> Get GitHub secret**. You use these values to configure the webhook in GitHub. 

    ![Review the function code](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png) 
         
Next, you create a webhook in your GitHub repository. 

## Configure the webhook
1. In GitHub, navigate to a repository that you own. You can also use any repository that you have forked. If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>. 
 
2. Click **Settings**, then click **Webhooks**, and  **Add webhook**.
   
    ![Add a GitHub webhook](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

3. Use settings as specified in the table, then click **Add webhook**.
 
    ![Set the webhook URL and secret](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

    | Setting      |  Suggested value   | Description                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Payload URL** | Copied value | Use the value returned by  **</> Get function URL**. |
    | **Secret**   | Copied value | Use the value returned by  **</> Get GitHub secret**. |
    | **Content type** | application/json | The function expects a JSON payload. |
    | Event triggers | Let me select individual events | We only want to trigger on issue comment events.  |
    |                | Issue comment                    |  |

Now, the webhook is configured to trigger your function when a new issue comment is added. 

## Test the function
1. In your GitHub repository, open the **Issues** tab in a new browser window.

2. In the new window, click **New Issue**, type a title, and then click **Submit new issue**. 

2. In the issue, type a comment and click **Comment**. 

    ![Add a GitHub issue comment.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png) 

3. Go back to the portal and view the logs. You should see a trace entry with the new comment text. 
    
     ![View the comment text in the logs.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)
 

## Clean up resources

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## Next steps

You have created a function that runs when a request is received from a GitHub webhook. 
[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md). 



