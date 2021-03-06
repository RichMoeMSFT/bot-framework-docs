---
title: Add suggested actions to messages | Microsoft Docs
description: Learn how to add suggested actions to messages using the Bot Builder SDK for .NET.
author: kbrandl
ms.author: v-kibran
manager: rstand
ms.topic: article
ms.prod: bot-framework
ms.date: 05/12/2017
ms.reviewer: 
---

# Add suggested actions to messages
> [!div class="op_single_selector"]
> - [.NET](../dotnet/bot-builder-dotnet-add-suggested-actions.md)
> - [Node.js](../nodejs/bot-builder-nodejs-send-suggested-actions.md)
> - [REST](../rest-api/bot-framework-rest-connector-add-suggested-actions.md)

[!include[Introduction to suggested actions](~/includes/snippet-suggested-actions-intro.md)] 

> [!TIP]
> To learn how various channels render suggested actions, see the [Channel Inspector][channelInspector].

## Send suggested actions

To add suggested actions to a message, set the `SuggestedActions` property of the activity to a list of [CardAction][cardAction] objects that represent the buttons to be presented to the user. 

This code example shows how to create a message that presents three suggested actions to the user:

[!code-csharp[Add suggested actions](~/includes/code/dotnet-add-suggested-actions.cs#addSuggestedActions)]

When the user taps one of the suggested actions, the bot will receive a message from the user that contains the `Value` of the corresponding action.

## Additional resources

- [Activities overview](~/dotnet/bot-builder-dotnet-activities.md)
- [Create messages](~/dotnet/bot-builder-dotnet-create-messages.md)
- <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.bot.connector.activity?view=botbuilder-3.8" target="_blank">Activity class</a>
- <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.bot.connector.imessageactivity?view=botbuilder-3.8" target="_blank">IMessageActivity interface</a>
- <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.bot.connector.cardaction?view=botbuilder-3.8" target="_blank">CardAction class</a>
- <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.bot.connector.suggestedactions?view=botbuilder-3.8" target="_blank">SuggestedActions class</a>

[channelInspector]: https://docs.botframework.com/en-us/channel-inspector/channels/Facebook/#navtitle

[cardAction]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.bot.connector.cardaction?view=botbuilder-3.8