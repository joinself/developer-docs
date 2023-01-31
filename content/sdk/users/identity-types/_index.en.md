---
title: "Identity types"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 2
draft: false
# search related keywords
keywords: ["identity", "app", "public keys", "devices"]
---

Self network is formed of different entities with the ability to interact between them.

We name these entities **identities** and they own a **_self_id_**, an **array of _device ids_** and an array of **_public keys_**.

An identity can only communicate with another identity if _IdentityA_ is a connection of _IdentityB_. If this connection is in place _IdentityA_ will be able to request the _IdentityB_ properties _(device_ids and public keys)_ to interact with it.

At the moment identities can be divided into users and apps.

### Getting the public keys

Every single identity on the _Self_ network has at least one public key assigned to it. Lets see how you can get the public keys related to a _Self_ user.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @user = @client.identity.public_key "1112223334", "1"
    {{% /tab %}}

    {{% tab "Go" %}}
    identity, _ := client.IdentityService().GetPublicKey("1112223334", "1")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let key = await client.identity().publicKey("1112223334", "1")
    {{% /tab %}}
{{% /tabs %}}


### Identity devices

Same as with public keys each identity has at least one device.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @devices = @client.identity.devices "1112223334"
    {{% /tab %}}

    {{% tab "Go" %}}
    devices _ := client.IdentityService().GetDevices("1112223334")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let devices = await client.identity().devices("1112223334")
    {{% /tab %}}
{{% /tabs %}}