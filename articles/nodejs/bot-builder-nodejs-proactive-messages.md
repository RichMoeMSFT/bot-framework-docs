---
title: Send proactive messages | Microsoft Docs
description:  LEarn how to interrupt the current conversation flow with a proactive message using the Bot Builder SDK for Node.js
author: kbrandl
ms.author: v-kibran
manager: rstand
ms.topic: article
ms.prod: bot-framework
ms.date: 
ms.reviewer:
---
# Send proactive messages
> [!div class="op_single_selector"]
> - [.NET](../dotnet/bot-builder-dotnet-proactive-messages.md)
> - [Node.js](../nodejs/bot-builder-nodejs-proactive-messages.md)

[!include[Introduction to proactive messages - part 1](~/includes/snippet-proactive-messages-intro-1.md)] 

## Types of proactive messages

[!include[Introduction to proactive messages - part 2](~/includes/snippet-proactive-messages-intro-2.md)] 

## Send an ad hoc proactive message

The following code samples show how to send an ad hoc proactive message by using the Bot Builder SDK for Node.js.

To be able to send an ad hoc message to a user, the bot must first collect and save information about the user from the current conversation. 
The **address** property of the message includes all of the information that the bot will need to send an ad hoc message to the user later. 

```javascript
bot.dialog('/', function(session, args) {
    var savedAddress = session.message.address;

     // (Save this information somewhere that it can be accessed later, such as in a database.)

    var message = 'Hello user, good to meet you! I now know your address and can send you notifications in the future.';
    session.send(message);
})
```

> [!NOTE]
> For simplicity, this example does not specify how to store the user data. 
> The bot can store the user data in any manner as long as the bot can access it later.

After the bot has collected information about the user, it can send an ad hoc proactive message to the user at any time. 
To do so, it simply retrieves the user data that it stored previously, constructs the message, and sends it.

```javascript
var bot = new builder.UniversalBot(connector);

function sendProactiveMessage(address) {
    var msg = new builder.Message().address(address);
    msg.text('Hello, this is a notification');
    msg.textLocale('en-US');
    bot.send(msg);
}
```

> [!TIP]
> An ad hoc proactive message can be initiated like from 
> asynchronous triggers such as http requests, timers, queues or from anywhere else that the developer chooses.

## Send a dialog-based proactive message

The following code samples show how to send a dialog-based proactive message by using the Bot Builder SDK for Node.js.

To be able to send a dialog-based message to a user, the bot must first collect (and save) information from the current conversation. 
The **address** property of the message includes all of the information that the bot will need to send an dialog-based proactive message to the user. 

```javascript
bot.dialog('/', function(session, args) {
    var savedAddress = session.message.address;

     // (Save this information somewhere that it can be accessed later, such as in a database.)

    var message = 'Hello user, good to meet you! I now know your address and can send you notifications in the future.';
    session.send(message);
})
```

When it is time to send the message, the bot creates a new dialog and adds it to the top of the dialog stack. The new dialog takes control of the conversation, delivers the proactive message, closes, and then returns control to the previous dialog in the stack. 

```javascript
function startProactiveDialog(addr) {
    // Set resume:true to resume the previous dialog;
    // else, set resume:false to resume at the root dialog.
    bot.beginDialog(savedAddress, "*:/survey", {}, { resume: true });  
}
```

> [!NOTE]
> The code sample above requires a custom file: **botadapter.js**. 
> You can find a copy of that file [here](https://trpp24botsamples.visualstudio.com/_git/Code?path=%2FNode%2Fcore-proactiveMessages%2FstartNewDialog%2Fbotadapter.js&version=GBmaster&_a=contents).

The survey dialog controls the conversation until it finishes. 
Then, it closes (by calling `session.endDialog()`), thereby returning control back to the previous dialog. 


```javascript
bot.dialog('/survey', [
    function (session, args, next) {
        if (session.message.text=="done"){
            session.send("Great, back to the original conversation");
            session.endDialog();
        }else{
            session.send('Hello, I\'m the survey dialog. I\'m interrupting your conversation to ask you a question. Type "done" to resume');
        }
    },
    function (session, results) {
    }
]);
```

## Sample code

For a complete sample that shows how to send proactive messages using the Bot Builder SDK for Node.js, see the <a href="https://github.com/Microsoft/BotBuilder-Samples/tree/master/Node/core-proactiveMessages" target="_blank">Proactive Messages sample</a> in GitHub. 
Within the Proactive Messages sample, <a href="https://github.com/Microsoft/BotBuilder-Samples/tree/master/Node/core-proactiveMessages/simpleSendMessage" target="_blank">simpleSendMessage</a> shows how to send an ad-hoc proactive message and <a href="https://github.com/Microsoft/BotBuilder-Samples/tree/master/Node/core-proactiveMessages/startNewDialog" target="_blank">startNewDialog</a> shows how to send a dialog-based proactive message.

## Additional resources

- [Designing conversation flow](~/bot-design-conversation-flow.md)
