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

### Response Fact Resquest

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    
    {{% /tab %}}

    {{% tab "Swift" %}}
    
    {{% /tab %}}    
{{% /tabs %}}

### Subscribe to Fact Request
Subscribing to a fact request

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    account.setOnRequestListener { message ->        
        if (message is AttestationRequest) {
            Timber.d("AttestationRequest from:${message.fromIdentifier()} - facts: ${message.facts().map { it.name() }}")
        }
    }
    {{% /tab %}}

    {{% tab "Swift" %}}
    self.account.setOnRequestListener { msg in     
        if let request = msg as? AttestationRequest {
            log.debug("AttestationRequest from:\(request.fromIdentifier()) - fact:\(request.facts().map{$0.name()})")
        }
    }
    {{% /tab %}}    
{{% /tabs %}}


### Subscribe to Fact Response
Subscribing to a fact response

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    account.setOnResponseListener { message ->        
        if (message is AttestationResponse) {
            Timber.d("AttestationRequest from:${message.fromIdentifier()} - attestation: ${message.attestations().size}")
        }
    }
    {{% /tab %}}

    {{% tab "Swift" %}}
    self.account.setOnResponseListener { msg in        
        if let response = msg as? AttestationResponse {
            log.debug("AttestationResponse from:\(response.fromIdentifier()) - status:\(response.status().rawValue) - attestation:\(response.attestations().map{$0.fact().value()})")
        }
    }
    {{% /tab %}}    
{{% /tabs %}}


