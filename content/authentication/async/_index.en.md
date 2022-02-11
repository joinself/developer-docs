---
title: "Async auth requests"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 3
draft: false
# search related keywords
keywords: [""]
---

This scenario is similar to non-blocking authentication, however, it’s not restricted to only one user.

Sending an asynchronous authentication request is pretty straightforward, you can do it with the _async_ option.

This will return a conversation id identifying the authentication conversation, you should store it and catch it on a subscription, check _Receiving authentication response - Subscribe_ section on how to manage this.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    cid = @client.
        authentication.
        request("1112223334", async: true)
    {{% /tab %}}

    {{% tab "Go" %}}
    client.
        AuthenticationService().
        RequestAsync("1112223334", "conversation_id")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await client.
        authentication().
        request("1112223334", { 'async': true })
    {{% /tab %}}
{{% /tabs %}}