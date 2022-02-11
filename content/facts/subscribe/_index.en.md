---
title: "Subscribe to fact response"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 6
draft: false
# search related keywords
keywords: ["fact", "facts", "request", "requests", "name", "email", "subscribe", "response"]
---

As the user also has the option to accept or reject a fact request, the response also comes with a status property and some helpers like the authentication response.

Additionally a fact response comes with a list of attestations for the requested fact.

Subscribing to a **facts** response is similar to authentication.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.facts.subscribe do |resp|
        # GOTO Deal with the response for details
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    // TBD
    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.facts().subscribe((res: any): any => {
        // GOTO Deal with the response for details
    })
    {{% /tab %}}
{{% /tabs %}}