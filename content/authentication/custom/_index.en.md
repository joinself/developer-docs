---
title: "Custom auth requests"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 3
draft: false
# search related keywords
keywords: [""]
---

Providing a _cid_ allows you to override the randomly generated _conversation id_ with your own, this is useful to keep track of conversations with a preset identifier, let’s see the asynchronous example using a custom cid.

Instead of using the randomly generated conversation identifier, we can force the system to use our own unique id.


{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.
        authentication.
        request("1112223334", cid: "conversation_id")
    {{% /tab %}}

    {{% tab "Go" %}}
    client.
        AuthenticationService().
        RequestAsync("1112223334", "conversation_id")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await client.
        authentication().
        request("1112223334", { 'cid': "conversation_id" })
    {{% /tab %}}
{{% /tabs %}}