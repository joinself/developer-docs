---
title: "Asynchronous"
date: 2022-02-09T11:05:05+06:00
lastmod: 2022-02-09T11:05:05+06:00
weight: 3
draft: false
# search related keywords
keywords: ["fact", "anonymous", "zero knowledge", "zero", "intermediary", "async"]
---

{{% tabs groupId="install" %}}
    {{% tab "Ruby" %}}
    res = @client.facts.request_via_intermediary(selfid, facts, async: true)
    {{% /tab %}}

    {{% tab "Go" %}}
    req := fact.IntermediaryFactRequest{
        SelfID:       os.Args[1],
        Intermediary: intermediary,
        Description:  "info",
        Facts: []fact.Fact{
            {
                Fact:          fact.FactEmail,
                Sources:       []string{fact.SourceUserSpecified},
                Operator:      "==",
                ExpectedValue: "test@example.com",
            },
        },
        Expiry: time.Minute * 5,
    }

    factService := client.FactService()

    resp, err := factService.RequestViaIntermediary(&req)
    if err != nil {
        log.Fatal("fact request returned with: ", err)
    }

    for _, f := range resp.Facts {
        if f.Result() != true {
            log.Fatal("intermediary could not verify the required facts")
        }
        log.Printf("Your assertion that %s %s is %t\n", f.Fact, f.Operator, f.Result())
    }
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await sdk.facts().requestViaIntermediary(selfID, facts, { 'async': true }
    {{% /tab %}}
{{% /tabs %}}

This will return a conversation id identifying the fact request conversation, you should store it and catch it on a subscription, as described on the next section.
