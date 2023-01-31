---
title: "Connections"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 1
draft: false
# search related keywords
keywords: ["identity", "app", "connect", "disconnect", "permit", "block"]
toc: true
---

### Permit connections

Allows incoming messages from specified identities.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.messaging.permit_connection "1234567890"
    {{% /tab %}}

    {{% tab "Go" %}}
    err := selfsdk.MessagingService().PermitConnection("1234567890")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let success = await sdk.messaging().permitConnection("1234567890")
    {{% /tab %}}
{{% /tabs %}}

{{< notice note >}}Permitting incomming connections only applies if you don't have a global connection (*) permission. If you do, you have to revoke it first.{{</ notice >}}


### Permit global connections

You can permit connections from everyone using an “*”.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.messaging.permit_connection "*"
    {{% /tab %}}

    {{% tab "Go" %}}
    err := selfsdk.MessagingService().PermitConnection("*")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let success = await sdk.messaging().permitConnection("*")
    {{% /tab %}}
{{% /tabs %}}


###  Revoke specific connection

You can also revoke connections from a specific self identifier with:

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.messaging.revoke_connection "1234567890"
    {{% /tab %}}

    {{% tab "Go" %}}
    err := client.MessagingService().RevokeConnection("1234567890")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let success = await sdk.messaging().revokeConnection("1234567890")
    {{% /tab %}}
{{% /tabs %}}

{{< notice note >}}Revoking a connection only applies if you don't have a global connection (*) permission setup. If you do, you have to revoke it first.{{</ notice >}}


### Revoke global connections

Revoke connection permissions from everyone using an “*”.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.messaging.revoke_connection "*"
    {{% /tab %}}

    {{% tab "Go" %}}
    err := client.MessagingService().RevokeConnection("*")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let success = await sdk.messaging().revokeConnection("*")
    {{% /tab %}}
{{% /tabs %}}

### Listing connections

You can list your app allowed connections.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.messaging.allowed_connections.each do |self_id|
    p "- '#{self_id}'"
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    connections, _ := client.MessagingService().ListConnections()
    log.Println("connected to:", connections)
    {{% /tab %}}

    {{% tab "Typescript" %}}
    conns = await sdk.messaging().allowedConnections()
    sdk.logger.info(` - connections : ${conns.join(",")}`)
    {{% /tab %}}
{{% /tabs %}}