---
title: "Send and receive messages"
date: 2022-02-09T11:05:05+06:00
lastmod: 2022-02-09T11:05:05+06:00
weight: 1
draft: false
# search related keywords
keywords: ["messaging", "message", "messages"]
---

Self SDK allows you to send messages to any identity on self network, this includes users, orgs and apps.

The interface used to interact with messaging is chat service, let's see how can we create an app automatically responding all ping messages with a pong.

{{% tabs %}}
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

Easy, isn't it? As you can see, you can use the chat service `message` method to send messages to a specific user, and `on_message` to receive them. 

The object representing a message has also some handy methods to interact with that message, included sending a new message to the same conversation with `message(body)`.

Let's have a closer look at all the options you have when sending and receiving messages

### Sending messages

The interface for sending a normal message is quite simple, just provide the user and text you want to send and that's it. 

However, the system provides some useful options you can pass to this method. Let's have a look at the most important ones.

{{% tabs %}}
    {{% tab "Ruby" %}}
    @app.chat.message user, "ready!", gid: "group_id",
                                      rid: "uuid",
    {{% /tab %}}

    {{% tab "Go" %}}
    client.ChatService().Message(user, "ready!", chat.MessageOptions{
        GID: "group_id",
        RID: "uuid,
    }
    {{% /tab %}}

    {{% tab "Typescript" %}}
    client.chat().message user, "ready!", {
        "gid": "group_id",
        "rid": "uuid"
    }
    {{% /tab %}}
{{% /tabs %}}

### gid

You'll see `gid` option supported across different methods, `gid` refers to group id, and when provided will indicate the other client the current conversation is a group conversation instead of a 1 to 1 chat.

Usually this id is not used directly through this method, and instead the message is sent through a helper on Group object, check [Groups](/messaging/groups) for more details.

### rid

In this case `rid` is used to refer a previous message by it's `jti`, once the other party receives a `rid` as part of the payload it will interpret is a direct response to a specific message, and it will be displayed accordingly. 

![image example](rid.png "Message reply")

If you've already received a message you want to respond, you can do it directly through the respond method like:

{{% tabs %}}
    {{% tab "Ruby" %}}
    @app.chat.on_message do |msg|
        msg.respond "I like this"
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    client.ChatService().OnMessage(func(cm *chat.Message) {
        cm.Respond("I like this")
    })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.chat().OnMessage(async (cm: ChatMessage) => {
        cm.respond("I like this")
    })
    {{% /tab %}}
{{% /tabs %}}