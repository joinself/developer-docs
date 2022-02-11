---
title: "Notify"
date: 2017-12-27T11:02:05+06:00
icon: "ti-bell"
description: "Zero knowledge proofs"
type : "docs"
keywords: ["notify", "notifications", "push notification"]
---

It prompts the user with a push notification or badge with a specific message. The message will be available on the notifications screen.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.messaging.notify "1234567890", "Hello world!"
    {{% /tab %}}

    {{% tab "Go" %}}
    err := client.MessagingService().Notify("1234567890", "Hello world!")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    await sdk.messaging().notify("1234567890", "Hello world!")
    {{% /tab %}}
{{% /tabs %}}