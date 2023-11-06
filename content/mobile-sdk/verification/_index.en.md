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

#### Driving License
Self verification requires front and back images of driving license.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    val front = DataObject.Builder()
        .setData(<front image bytes>)
        .setContentType("image/jpeg")
        .build()
    val back = DataObject.Builder()
        .setData(<back image bytes>)
        .setContentType("image/jpeg")
        .build()
    val proofs = mapOf(DocumentDataType.DOCUMENT_IMAGE_FRONT to front,
                        DocumentDataType.DOCUMENT_IMAGE_BACK to back)
    val verificationRequest = VerificationRequest.Builder()
        .setType(DocumentType.DRIVING_LICENSE)
        .setProofs(proofs)
        .build()
    account.send(verificationRequest) { }    
    {{% /tab %}}

    {{% tab "Swift" %}}
    var proofs: [String: DataObject] = [:]    
    let front = DataObject.Builder()
        .withData(<front image data>)
        .withContentType("image/jpeg")
        .build()
    proofs[DocumentDataType.DOCUMENT_IMAGE_FRONT] = front
    let back = DataObject.Builder()
        .withData(<back image data>)
        .withContentType("image/jpeg")
        .build()
    proofs[DocumentDataType.DOCUMENT_IMAGE_BACK] = back    
    let verificationRequest = VerificationRequest.Builder()
        .withType(DocumentType.DRIVING_LICENSE)
        .withProofs(proofs)
        .build()
    Task {
        try await account.send(message: verificationRequest, onAcknowledgement: {error in
        })
    }
    {{% /tab %}}    
{{% /tabs %}}

#### ID Card
Self verification requires front and back images and mrz text of ID Card.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    val front = DataObject.Builder()
        .setData(<front image bytes>)
        .setContentType("image/jpeg")
        .build()
    val back = DataObject.Builder()
        .setData(<back image bytes>)
        .setContentType("image/jpeg")
        .build()
    val mrz = DataObject.Builder()
        .setData("IDGBR1234567897<<<<<<<<<<<<<<<7704145F1907313GBR<<<<<<<<K<<8TEST<<USER<<<<<<<<<<".toByteArray())
        .setContentType("text/plain")
        .build()
    val proofs = mapOf(DocumentDataType.DOCUMENT_IMAGE_FRONT to front,
                        DocumentDataType.DOCUMENT_IMAGE_BACK to back,
                        DocumentDataType.MRZ to mrz)
    val verificationRequest = VerificationRequest.Builder()
        .setType(DocumentType.IDCARD)
        .setProofs(proofs)
        .build()
    account.send(verificationRequest) { }    
    {{% /tab %}}

    {{% tab "Swift" %}}
    var proofs: [String: DataObject] = [:]    
    let front = DataObject.Builder()
        .withData(<front image data>)
        .withContentType("image/jpeg")
        .build()
    proofs[DocumentDataType.DOCUMENT_IMAGE_FRONT] = front
    let back = DataObject.Builder()
        .withData(<back image data>)
        .withContentType("image/jpeg")
        .build()
    proofs[DocumentDataType.DOCUMENT_IMAGE_BACK] = back    
    if let data = "IDGBR1234567897<<<<<<<<<<<<<<<7704145F1907313GBR<<<<<<<<K<<8TEST<<USER<<<<<<<<<<".data(using: .utf8) {
        let mrz = DataObject.Builder()
            .withData(data)
            .withContentType("text/plain")
            .build()
        proofs[DocumentDataType.MRZ] = mrz
    }
    let verificationRequest = VerificationRequest.Builder()
        .withType(DocumentType.IDCARD)
        .withProofs(proofs)
        .build()
    Task {
        try await account.send(message: verificationRequest, onAcknowledgement: {error in
        })
    }
    {{% /tab %}}    
{{% /tabs %}}

#### Passport
Self verification requires data files in NFC chip.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    val dg1 = DataObject.Builder()
        .setData(<dg1 file bytes>)
        .setContentType("application/x-binary")
        .build()
    val dg2 = DataObject.Builder()
        .setData(<dg2 file bytes>)
        .setContentType("application/x-binary")
        .build()
    val sod = DataObject.Builder()
        .setData(<sod file bytes>)
        .setContentType("application/x-binary")
        .build()
    val proofs = mapOf(DocumentDataType.DG1 to dg1,
        DocumentDataType.DG2 to dg2,
        DocumentDataType.SOD to sod)            
    val verificationRequest = VerificationRequest.Builder()
        .setType(DocumentType.PASSPORT)
        .setProofs(proofs)
        .build()
    account.send(verificationRequest) { }    
    {{% /tab %}}

    {{% tab "Swift" %}}
    var proofs: [String: DataObject] = [:]    
    let dg1 = DataObject.Builder()
        .withData(<dg1 file data>)
        .withContentType("application/x-binary")
        .build()
    proofs[DocumentDataType.DG1] = dg1
    let dg2 = DataObject.Builder()
        .withData(<dg2 file data>)
        .withContentType("application/x-binary")
        .build()
    proofs[DocumentDataType.DG2] = dg2
    let sod = DataObject.Builder()
        .withData(<sod file data>)
        .withContentType("application/x-binary")
        .build()
    proofs[DocumentDataType.SOD] = sod
    let verificationRequest = VerificationRequest.Builder()
        .withType(DocumentType.PASSPORT)
        .withProofs(proofs)
        .build()
    Task {
        try await account.send(message: verificationRequest, onAcknowledgement: {error in
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
