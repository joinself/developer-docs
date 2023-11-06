---
title: "Verification"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Documentation verification"
type : "docs"
weight: 7
---

### Verification Request
Sending a verification request to Self verification server.

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
        .toIdentifier("24520674618")
        .withFacts([fact])
        .build()
    Task {
        try await account.send(message: factRequest, onAcknowledgement: {error in
        })
    }
    {{% /tab %}}    
{{% /tabs %}}

### Verification Response
Subscribing to responses from Self verification server.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    account.setOnResponseListener { message ->        
        if (message is VerificationResponse) {
            Timber.d("VerificationResponse from:${message.fromIdentifier()} - attestation: ${message.attestations().size}")
        }
    }
    {{% /tab %}}

    {{% tab "Swift" %}}
    self.account.setOnResponseListener { msg in        
        if let response = msg as? VerificationResponse {
            log.debug("VerificationResponse from:\(response.fromIdentifier()) - status:\(response.status().rawValue) - attestation:\(response.attestations().map{$0.fact().value()})")
        }
    }
    {{% /tab %}}    
{{% /tabs %}}
