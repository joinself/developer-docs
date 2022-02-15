---
title: "Attachments / objects"
date: 2022-02-09T11:05:05+06:00
lastmod: 2022-02-09T11:05:05+06:00
weight: 4
draft: false
# search related keywords
keywords: ["messaging", "message", "messages", "attachments", "object", "image", "file"]
---

Sharing an image, a document or just a gif is an important part of your users daily messaging, the SDK allows your app to send this kind of messages as well. Let's see how.

### Public objects

Most of the time we only share public images, and in this case we don't require the document to be encrypted, so we can directly share the URL.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    opts = { objects: [{ 
        link: "https://user-images.githubusercontent.com/14011726/94132137-7d4fc100-fe7c-11ea-8512-69f90cb65e48.gif", 
        name: "homer",
        mime: "image/gif",
    }] }
    client.message user, "ready!", opts
    {{% /tab %}}

    {{% tab "Go" %}}
	obj := chat.MessageObject{
		Name: "Hello",
		Link: "https://user-images.githubusercontent.com/14011726/94132137-7d4fc100-fe7c-11ea-8512-69f90cb65e48.gif",
		Mime: "image/gif",
	}
	m, err = client.ChatService().Message([]string{os.Args[1]}, "no way...", chat.MessageOptions{
		Objects: []chat.MessageObject{obj},
	})    
    {{% /tab %}}

    {{% tab "Typescript" %}}
    opts = { "objects": [{
        "link": "https://user-images.githubusercontent.com/14011726/94132137-7d4fc100-fe7c-11ea-8512-69f90cb65e48.gif", 
        "name": "homer",
        "mime": "image/gif",
    }]}
    client.chat().message user, "ready!", opts)
    {{% /tab %}}
{{% /tabs %}}


### Non-public objects

All non-public objects shared between identities are encrypted by default using [Poly1305](https://en.wikipedia.org/wiki/Poly1305). This encryption layer is built on the SDK, so should be transparent for end users. Let's see how we can send a local file.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    URI.open(path) do |image|
        name = "image.#{path.split(".").last}"
        mime = "image/#{path.split(".").last}"
        msg.message("your image sir...", objects: [{ name: name,
                                                     data: image.read,
                                                     mime: mime }])
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    data, err := os.ReadFile("/tmp/dat")
    check(err)
	m, err = cs.Message([]string{os.Args[1]}, "your file sir...", chat.MessageOptions{
		Objects: []chat.MessageObject{chat.MessageObject{
		Name: "image.gif",
		Data: data,
		Mime: "image/gif",
	    }},
	})    
    {{% /tab %}}

    {{% tab "Typescript" %}}
    import * as fs from 'fs';
    let data = fs.readFileSync('foo.txt','utf8');
    client.chat().message user, "your file sir...", { "objects": [{
        "data": data, 
        "name": "image.gif",
        "mime": "image/gif",
    }]})
    {{% /tab %}}
{{% /tabs %}}