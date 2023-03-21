---
title: "Starting the client"
date: 2022-02-09T11:02:05+06:00
lastmod: 2022-02-09T11:02:05+06:00
weight: 3
draft: false
# search related keywords
keywords: ["install", "setup", "start"]
---


### Starting your client

At this point you may have your client setup, but it's not yet ready or connected to self network.

In order to be able to send an receive messages from the Self Network you'll need to call start on your client.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.start
    {{% /tab %}}

    {{% tab "Go" %}}
    client.Start()
    {{% /tab %}}

    {{% tab "Typescript" %}}
    client.start()
    {{% /tab %}}
{{% /tabs %}}

A separated approach for initialize and start your client allows you to subscribe to certain events before the connection has started, and avoid missing some incoming messages.
