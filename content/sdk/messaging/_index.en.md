---
title: "Messaging"
date: 2022-02-15T11:02:05+06:00
icon: "ti-comment"
description: "Interact with your users through messaging"
type : "product"
weight: 5
---

The Self SDK provides a comprehensive set of messaging capabilities, allowing developers to integrate **secure** and **privacy-focused** communication features into their applications. 

With Self, you can enable **end-to-end encrypted messaging** between users, support **group messaging**, exchange **encrypted attachments**, and implement various message actions. 

This documentation describes the features, functionalities, and implementation details of the Self SDK.

### Implementation Example

Simple ping-pong messaging example

{{% tabs groupId="install" %}}
    {{% tab "Ruby" %}}
    @app.chat.on_message do |msg|
        if msg.body == "ping
            msg.message "pong"
        end
    end
    @app.chat.message user, "ready!"
    {{% /tab %}}

    {{% tab "Go" %}}
    client.ChatService().OnMessage(func(cm *chat.Message) {
        if cm.Body == "ping" {
            cm.Message("pong")
        }
    })
    @app.chat.message user, "ready!"
    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.chat().OnMessage(async (cm: ChatMessage) => {
        if (cm.body == "ping") {
            cm.message("pong")
        }
    })
    @app.chat.message user, "ready!"
    {{% /tab %}}
{{% /tabs %}}
### Privacy-Focused

The Self SDK prioritizes privacy by employing **end-to-end encryption** for all communications. 

This ensures that only the sender and the intended recipient of the messages have access to the shared data. 

The SDK implements industry-standard encryption algorithms and protocols, ensuring that sensitive user information remains secure and protected.

### Easy Integration

Implementing the Self SDK into your application is straightforward, enabling you to quickly enhance your communication capabilities. 

The SDK provides a simple and intuitive API, allowing developers to seamlessly integrate messaging features into their existing codebase. 

With comprehensive documentation and code examples, the integration process becomes smooth and hassle-free.

[Text messages API](/sdk/messaging/text-messages)

### Group Messaging

The Self SDK includes built-in support for group messaging, enabling users to participate in secure conversations with multiple participants. 

Developers can easily create and manage groups, invite users, and facilitate encrypted messaging among group members. 

The SDK's group messaging functionality ensures that communication within groups is private and protected.

[Group management docs](/sdk/messaging/groups)

### Attachments

With the Self SDK, you can enrich your messaging experience by exchanging encrypted chat objects such as documents, images, and other attachments. 

The SDK provides a convenient interface for attaching files to messages, ensuring the secure transmission of sensitive information. 

Whether it's sharing important documents or captivating images, the Self SDK allows users to exchange attachments with peace of mind.

[Attachments docs](/sdk/messaging/objects)

### Message Actions

The Self SDK offers a range of message actions that developers can implement to enhance the messaging experience. 

These actions include marking messages as **received** or **read**, **modifying message** content, and **deleting** messages. 

By implementing message actions, users can have more control over their conversations, ensuring that messages accurately reflect their communication status and preferences.

### Conclusion

The Self SDK empowers developers to integrate robust and privacy-focused messaging capabilities into their applications. 

With end-to-end encryption, easy integration, group messaging support, attachment exchange, and flexible message actions, the SDK provides a **comprehensive solution for secure communication**. 

By leveraging the Self SDK, developers can enhance their applications with privacy-focused messaging features, creating a **secure and reliable communication platform** for their users.