---
title: "Non-blocking requests"
date: 2022-02-09T11:05:05+06:00
lastmod: 2022-02-09T11:05:05+06:00
weight: 2
draft: false
# search related keywords
keywords: ["fact", "anonymous", "zero knowledge", "zero", "intermediary", "non-blocking"]
---

{{% tabs %}}
    {{% tab "Ruby" %}}
    @client.facts.request_via_intermediary(selfid, facts) do |res|
        # GOTO Receiving fact response - Deal with the response
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    // use language built in goroutines
    go func() {
        // ...
    }
    {{% /tab %}}

    {{% tab "Typescript" %}}
    // use language built in async
    async() => {
        // ...
    }
    {{% /tab %}}
{{% /tabs %}}