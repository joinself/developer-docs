---
title: "Accounts"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Create account in Self network"
type : "docs"
weight: 3
---

### Create an account
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

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    account.close()    
    {{% /tab %}}

    {{% tab "Swift" %}}
    account.close()    
    {{% /tab %}}    
{{% /tabs %}}