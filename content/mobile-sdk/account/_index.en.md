---
title: "Accounts"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Create account in Self network"
type : "docs"
weight: 3
---


Account is the main interface to Self network.  
Account holds SelfId and keypair that used to interact with other accounts in Self network.


### Create an account
By creating an account, Self network will generate a SelfId for this account.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    val selfId = account.register(attestation)    
    {{% /tab %}}

    {{% tab "Swift" %}}
    let selfId = await account.register(attestation: attestation)
    log.debug("SelfId: \(selfId)")
    {{% /tab %}}    
{{% /tabs %}}


### Close account
Self network will delete SelfId in the Self network and clean up local storage.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    account.close()    
    {{% /tab %}}

    {{% tab "Swift" %}}
    account.close()    
    {{% /tab %}}    
{{% /tabs %}}