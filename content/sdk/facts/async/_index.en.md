---
title: "Asynchronous fact request"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 3
draft: false
# search related keywords
keywords: ["fact", "facts", "request", "requests", "name", "email", "async"]
---
The asynchronous approach can be used in scenarios like the previous one, however it has a subtle difference, you have a single observer for all information requests, which can be useful in some situations as you can have all the logic centralized on a single point.



{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    cid = @client.facts.request(selfid, [SelfSDK::FACT_EMAIL], async: true)
    {{% /tab %}}

    {{% tab "Go" %}}
    req := fact.FactRequestAsync{
    SelfID:          selfID,
        Description: "info",
        Facts:       []fact.Fact{{ Fact: fact.FactEmail }},
        Expiry:      time.Minute * 5,
        CID:         "conversation_id",
    }

    resp, err := client.FactService().RequestAsync(&req)
    if err != nil {
        return "", err
    }
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await sdk.facts().request(selfID, [{ fact: 'email_address' }], { async: true })
    {{% /tab %}}
{{% /tabs %}}