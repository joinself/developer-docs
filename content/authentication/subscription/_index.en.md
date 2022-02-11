---
title: "Subscribe to responses"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 5
draft: false
# search related keywords
keywords: [""]
---

Users can respond to authentication requests by accepting or rejecting them. On the other hand, you won’t receive asynchronous notifications for requests which have timed out.

You can subscribe to authentication responses with this snippet

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.authentication.subscribe do |auth_res|
        puts resp.status
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    client.MessagingService().Subscribe("identities.authenticate.req", func(m *messaging.Message)) {
        // manage the response
    }
    {{% /tab %}}

    {{% tab "Typescript" %}}
    client.messaging().subscribe("identities.authenticate.req", (res: any): any => {
        // manage the response
    })
    {{% /tab %}}
{{% /tabs %}}