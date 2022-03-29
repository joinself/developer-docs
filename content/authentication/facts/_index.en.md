---
title: "Auth with facts"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 7
draft: false
# search related keywords
keywords: ["auth", "facts", "request", "registration"]
---

Many times, specially on a registration process you want your users to authenticate and at the same time you require some sort of specific facts, for example name or email.

Facts service allows you to send a fact request with the form of an authentication, with the option `auth`

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    cid = @client.facts.request(selfid, [SelfSDK::FACT_EMAIL], async: true, auth: true)
    {{% /tab %}}

    {{% tab "Go" %}}
    req := fact.FactRequest{
    SelfID:          selfID,
        Description: "info",
        Facts:       []fact.Fact{{ Fact: fact.FactEmail }},
        Expiry:      time.Minute * 5,
        Async:       true,
        CID:         "conversation_id",
        Auth:        true,
    }

    resp, err := client.FactService().RequestAsync(&req)
    if err != nil {
        return "", err
    }
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await sdk.facts().request(selfID, [{ fact: 'email_address' }], { async: true, auth: true })
    {{% /tab %}}
{{% /tabs %}}