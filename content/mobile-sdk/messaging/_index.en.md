---
title: "Messaging"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Send and receive messages"
type : "docs"
weight: 5
---

### Send Messages
{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    val attachment = Attachment.Builder()
        .setData("test data".toByteArray())
        .setName("test.txt")
        .build()
    val chatMsg = ChatMessage.Builder()
        .setToIdentifier("24520674618")
        .setMessage("hello")
        .setAttachments(listOf(attachment))
        .build()
    account.send(message = chatMsg) {
    }
    {{% /tab %}}

    {{% tab "Swift" %}}
    var attachments: [Attachment] = []
    if let data = "test data".data(using: .utf8) {
        let attachment = Attachment.Builder()
            .withData(data)
            .withName("test.txt")
            .build()
        attachments.append(attachment)
    }            
    let chatMsg = ChatMessage.Builder()
        .toIdentifier("58141443814")
        .withMessage("hello")
        .withAttachments(attachments)
        .build()                
    account.send(message: chatMsg, onAcknowledgement: {error in        
    })
    {{% /tab %}}    
{{% /tabs %}}

### Attachments

#### Upload

#### Download