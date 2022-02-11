---
title: "Disconnecting"
date: 2022-02-09T11:02:05+06:00
lastmod: 2022-02-09T11:02:05+06:00
weight: 4
draft: false
# search related keywords
keywords: ["setup", "disconnecting", "shut down", "stop", "close"]
---

You should gracefully manage the client disconnection by calling `close` method. If a connection is not gracefully closed Self messaging servers will kill that connection after one minute.

{{% tabs groupId="install" %}}
    {{% tab "Ruby" %}}
    @client.close
    {{% /tab %}}

    {{% tab "Go" %}}
    client.Close()
    {{% /tab %}}

    {{% tab "Typescript" %}}
    client.close()
    {{% /tab %}}
{{% /tabs %}}
