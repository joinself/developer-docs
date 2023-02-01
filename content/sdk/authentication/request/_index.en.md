---
title: "Request"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 1
draft: false
# search related keywords
keywords: [""]
custom_title: "Authentication request<div class='subtitle'>Sending authentication requests by identifier</div>"
toc: true
---

Authentication allows you to verify a user by its ID without storing any other information about it.

On this example we will know in advance the user _Self Identifier_, you'll need to allow the user introduce its ID on your application so you can proceed with this request.

{{< notice note >}}Note that by default users won't be connected to your app, in those cases they won't be receiving any incoming request, so let them know they need to be connected in advance.{{</ notice >}}

### Blocking request

Let's see an easy example on how to implement an authentication workflow with the different Self SDKs.

On this example we will opt for a blocking approach, where the main execution line waits for the user response to continue.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    user = "1112223334"
    authenticated = @app.authentication.request(user).accepted?
    {{% /tab %}}

    {{% tab "Go" %}}
    user := "1112223334"
    if resp, err != client.AuthenticationService().Request(user); err != nil {
        println("authentication rejected")
        return
    }
    authenticated := resp.Accepted
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await client.authentication().request("1112223334")
    let authenticated = res.isAccepted()
    {{% /tab %}}
{{% /tabs %}}

The user will receive 

### Non-blocking request

In contrast to blocking auth requests, there are situations where you just want to continue your execution line and set up an observer to be executed as soon as a response is received.

Let's say you have a conventional registration process where you let your users register to your application by its email address but you delay the email confirmation until they get back to you. This allows your users to go through a quick registration process, while you delay the data confirmation process.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    # Request lets you pass a block to be executed once a response is received
    @client.authentication.request selfid do |auth|
        return auth.accepted? # The user has rejected the authentication
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    // Go language provides you with goroutines to
    // implement a non-blocking approach
    go func() {
        res, err != client.AuthenticationService().Request(selfid)
        if err != nil {
            println("authentication rejected")
            return
        }
        println(res.Accepted)
    }()
    {{% /tab %}}

    {{% tab "Typescript" %}}
    async() => {
    try {
        let res = await client.authentication().request("1112223334")
        if(res.isAccepted() == true) {
        client.logger.info(`${res.selfID} is now authenticated 🤘`)
        } else if(res.accepted == false) {
        client.logger.warn(`${res.selfID} has rejected your authentication request`)
        } else {
        client.logger.error(res.errorMessage)
        }
    } catch (error) {
        client.logger.error(error.toString())
    }
    }
    {{% /tab %}}
{{% /tabs %}}


### Asynchronous requests

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

{{< notice note >}}As you can see the asynchronously of this call is accomplished by an extra option or *modifier* Let's see on the next chapter what other modifiers provides the authentication workflow.{{</ notice >}}

