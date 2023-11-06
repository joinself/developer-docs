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
    val chatMsg = ChatMessage.Builder()
        .setToIdentifier("24520674618")
        .setMessage("hello")        
        .build()
    account.send(message = chatMsg) {
    }
    {{% /tab %}}

    {{% tab "Swift" %}}
    let chatMsg = ChatMessage.Builder()
        .toIdentifier("58141443814")
        .withMessage("hello")        
        .build()                
    account.send(message: chatMsg, onAcknowledgement: {error in        
    })
    {{% /tab %}}    
{{% /tabs %}}

### Attachments
Self allows to attach an array of attachments to a chat message. An attachment can be any file such as image, documentation.

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

### Receive Messages
Subscribing to messaging stream from Self server.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}    
    account.setOnMessageListener { message ->            
        if (message is ChatMessage) {
            Timber.d("chatMessage sender:${message.fromIdentifier()} - content: ${message.message()} - attachments: ${message.attachments().size}")
        }
    }
    {{% /tab %}}

    {{% tab "Swift" %}}
    self.account.setOnMessageListener { msg in     
        if let chatMsg = msg as? ChatMessage {
            log.debug("chatMessage sender:\(msg.fromIdentifier()) - content:\(chatMsg.message()) - attachments: \(chatMsg.attachments().count)")
        }
    }
    {{% /tab %}}    
{{% /tabs %}}

### Files
Self object server allows to store files in 7 days, the maximum size is 20MB.

#### Upload
Upload data object to Self object server.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}    
    // upload a simple text file
    val dataObject = DataObject.Builder()
        .setData("hello".toByteArray())
        .setContentType("text/plain")
        .build()
    val dataLink = account.upload(dataObject)
    {{% /tab %}}

    {{% tab "Swift" %}}
    // upload a simple text file
    if let data = "hello".data(using: .utf8) {
        let dataObject = DataObject.Builder()
            .withData(data)
            .withContentType("text/plain")
            .build()
        let dataLink = await account.upload(dataObject: dataObject)
    }
    {{% /tab %}}    
{{% /tabs %}}


#### Download
Download a data object from Self object server.
{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}    
    val data = account.download(dataLink)
    {{% /tab %}}

    {{% tab "Swift" %}}
    let data = try await account.download(dataLink: dataLink)
    {{% /tab %}}    
{{% /tabs %}}


