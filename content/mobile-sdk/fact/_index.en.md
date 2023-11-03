---
title: "Facts"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Request a fact and response to a fact request"
type : "docs"
weight: 6
---

### Fact Request
{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    val fact = Fact.Builder()
    .setName("email")
    .build()
    val factRequest = AttestationRequest.Builder()
        .setToIdentifier("24520674618")
        .setFacts(listOf(fact))
        .build()
    account.send(factRequest) {}
    {{% /tab %}}

    {{% tab "Swift" %}}
    let fact = Fact.Builder()
    .withName("email")
    .build()
    let factRequest = AttestationRequest.Builder()
        .toIdentifier(recipient)
        .withFacts([fact])
        .build()
    Task {
        try await account.send(message: factRequest, onAcknowledgement: {error in
        })
    }
    {{% /tab %}}    
{{% /tabs %}}

### Fact Response

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    val selfId = account.register(attestation)    
    {{% /tab %}}

    {{% tab "Swift" %}}
    let selfId = await account.register(attestation: attestation)
    log.debug("SelfId: \(selfId)")
    {{% /tab %}}    
{{% /tabs %}}
