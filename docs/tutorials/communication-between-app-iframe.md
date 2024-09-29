---
title: Communicate with an iFrame widget
description: Learn how to send and receive data from an iFrame widget in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

Cross-origin communication between a Studio app and an embedded [iFrame](../reference/widgets/iframe.md) widget can be achieved by sending messages. This page shows how to send messages between the application and an embedded iFrame widget.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] An iFrame widget configured to embed your app.

## Instructions

### Send messages to the iFrame widget

The iFrame widget serves as the communication bridge between Studio and the embedded app. To send messages from Studio to your embedded app follow these steps:

1. Use the global function [postWindowMessage](/reference/framework/global-functions.md#post-message) in your [JSObject](../writing-code-in-studio/using-jsobjects.md) or configure a post message action for your widget in the Properties pane. For example, to send a message on the click of a button widget, select the **Post message** action for the **onClick** event, add the message details in the **Message** field, and set the **Target** as the name of the iFrame widget (`iFrame1`). Alternatively, use the `postWindowMessage()` by enabling the JS as shown below:

```js
postWindowMessage("Message content", 'iFrame1', "<Studio_hosted_url>"); // (1)!
```

1. Replace the `Message content` with your actual message. Set the Target as an iFrame widget. Replace `iFrame1` with the name of the iFrame widget, and `<Studio_hosted_url>` with the Studio domain.

2. To receive the messages, use the `addEventListener()` method of the `window` object that adds an event listener in your parent app.

```js title="Add this code in the app that you've embedded in Studio using the iFrame widget"
const messageHandler = (event) => { // (1)!
     if(event) { // (2)!
     const messageReceived = event.data;
     console.log(messageReceived);
     //Add code to manipulate the received message
     }
};

    
window.addEventListener('message', messageHandler); // (3)!

// Remember to unlisten to the event when it's no longer needed
// For example, unlisten when you have successfully processed the message
// window.removeEventListener('message', messageHandler);
```

1. The message sent is available in the event object.
2. Read the message by using the `event.data` property.
3. Add the event listener to read the incoming message.

### Send messages to Studio

The iFrame widget also helps in sending messages to Studio from your embedded app. To send messages from your embedded app follow these steps:

1. Use the [postMessage()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) method of the `window` object. Add the below code snippet in your app to send a message:

```js title="Add this code to your embedded app"
function sendMessage(message) { // (1)!
     if(message) {
          window.parent.postMessage(message, "<Studio_hosted_url>"); // (2)!
     }
}
```

1. `message` is the content of the message that you want to send to Studio.
2. Send the message in postMessage. Replace the `<Studio_hosted_url>` with your Studio domain,

Call the `sendMessage()` function whenever you want to send a message. Alternatively, you can directly use `window.parent.postMessage(message, "<Studio_hosted_url>")` in your code.

2. To receive the message in Studio, configure the `onMessageReceived()` event of the iFrame widget in the Properties pane and show an alert or execute query by passing the received message. Read the received message using the `message` property of the iFrame widget (`iFrame1`) as shown below:

```js
{{ '{{iFrame1.message}}' }} // (1)!
```

1. `iFrame1` is the name of the iFrame widget. Replace it with the name of your iFrame widget.
You may also choose to execute actions by adding callbacks to the [**onMessageReceived**](/reference/widgets/iframe#onmessagereceived) event, like showing a success or a failure message.
