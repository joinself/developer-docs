---
title: "Modifiers"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 2
draft: false
# search related keywords
keywords: [""]
custom_title: "Authentication request modifiers<div class='subtitle'>Explore the different options an authentication request presents</div>"
toc: true
---

### Async

We've already covered this modifier on the <a href='{{< relref "request#asynchronous-requests" >}}'>Asynchronous authentication requests</a>.

It basically allows you to send an authentication request and ignore any responses.

This is usually used in combination with an <a href='{{< ref "/sdk/authentication/response" >}}'>Authentication response subscription</a>

This modifier accepts a *boolean*.
{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    cid = @client.
        authentication.
        request("1112223334", async: true)
    {{% /tab %}}

    {{% tab "Go" %}}
    // Given the language nature this modifier is not implemented on Go.
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await client.
        authentication().
        request("1112223334", { 'async': true })
    {{% /tab %}}
{{% /tabs %}}


### CID

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


### Expiration timeout

Providing _exp_timeout_ parameter permits modify the default expiration timeout of an authentication request, making it only valid for a custom time.

Its provided as an integer with the total amount of seconds you want to be valid.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.
        authentication.
        request("1112223334", exp_timeout: 20000)
    {{% /tab %}}

    {{% tab "Go" %}}
    // Not supported
    {{% /tab %}}

    {{% tab "Typescript" %}}
    // Not supported
    {{% /tab %}}
{{% /tabs %}}