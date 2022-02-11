---
title: "Non-blocking auth requests"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 2
draft: false
# search related keywords
keywords: [""]
---

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