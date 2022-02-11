---
title: "Message actions"
date: 2022-02-09T11:05:05+06:00
lastmod: 2022-02-09T11:05:05+06:00
weight: 2
draft: false
# search related keywords
keywords: ["messaging", "message", "messages", "attachments", "read", "delivered", "edit", "delete", "remove"]
---

In this section we will review what actions we can take to modify the message state. 

### Mark as received

When your app receives a message the sdk is marking it as received by default. This behavior can be changed by modifying passing a specific parameter to on_message, at the same time you can mark a message as read on your convenience, let's see how.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @app.chat.on_message mark_as_delivered: false do |msg|
        msg.mark_as_delivered # explicitly mark the message as delivered
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    client.ChatService().OnMessage(func(cm *chat.Message) {
        cm.MarkAsDelivered()
    }, chat.OnMessageOptions{ MarkAsDelivered: false })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.chat().OnMessage(async (cm: ChatMessage) => {
        cm.markAsDelivered()
    }, { 'mark_as_delivered': false })
    {{% /tab %}}
{{% /tabs %}}

{{< notice note >}}Default behavior for on_message is to mark the message as received as soon as it's received.{{</ notice >}}

### Mark as read

Similarly to the previous example, you can modify on_message to automatically mark all messages as read with a specific option.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @app.chat.on_message mark_as_read: true do |msg|
        # ...
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    client.ChatService().OnMessage(func(cm *chat.Message) {
        // ...
    }, chat.OnMessageOptions{ MarkAsRead: true })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.chat().OnMessage(async (cm: ChatMessage) => {
        // ...
    }, { 'mark_as_read': true })
    {{% /tab %}}
{{% /tabs %}}

Additionally you can explicitly mark a received message as read with your own logic.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @app.chat.on_message do |msg|
        msg.mark_as_read
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    client.ChatService().OnMessage(func(cm *chat.Message) {
        cm.MarkAsRead()
    })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.chat().OnMessage(async (cm: ChatMessage) => {
        cm.MarkAsRead()
    })
    {{% /tab %}}
{{% /tabs %}}


### Edit

For a message you've already sent you can modify its body.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    m = @app.chat.message user, "one"
    m.edit "two"
    {{% /tab %}}

    {{% tab "Go" %}}
    m := @app.chat.message user, "one"
    m.Edit("two")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let m = @app.chat.message user, "one"
    m.Edit("two")
    {{% /tab %}}
{{% /tabs %}}


{{< notice note >}}You're only allowed to modify your own messages.{{</ notice >}}

### Delete

Deleting a message is as simple as modifying it, but using `delete` method instead.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    m = @app.chat.message user, "one"
    m.delete
    {{% /tab %}}

    {{% tab "Go" %}}
    m := @app.chat.message user, "one"
    m.Delete()
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let m = @app.chat.message user, "one"
    m.Delete()
    {{% /tab %}}
{{% /tabs %}}

{{< notice note >}}You're only allowed to delete your own messages.{{</ notice >}}
