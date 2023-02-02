---
title: "Recurrent requests"
date: 2022-02-15T11:02:05+06:00
icon: "ti-loop"
description: "Do not store sensible data, request it"
type : "docs"
weight: 6
custom_title: "Recurrent request<div class='subtitle'>Allow recurrent requests for a defined period of time</div>"
toc: true
---

As we've seen on [Facts](facts/) section you can request user's verified sensible data through facts service.

This becomes really useful when you can use the data at the moment. However, if you need to access the same data periodically or some time in the future, you'll be forced to store it.

Self recurrent requests feature allows you to **access the same data for a specific period of time** without having to wait for user's acceptance, so you don't need to store it on your servers.

Recurrent requests looks exactly the same as a regular fact request, except it makes use of allowed_for modifier, let's see an example.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    ten_days = 10 * 60 * 60 * 60
    # Request email, with recurrent requests enabled for ten days
    res = @client.facts.request(user, [:email_address], allowed_for: ten_days)    
    # At this point the user will be prompted with a confirmation box to 
    # allow access its email for the next 10 days.
    #
    # If we send the same request again, it will be automatically shared by the device
    # without user interaction.
    res = @client.facts.request(user, [:email_address])
    {{% /tab %}}

    {{% tab "Go" %}}
    // Request email, with recurrent requests enabled for ten days
    resp, err := client.FactService().Request(&fact.FactRequest{
        SelfID:      selfID,
        Description: "info",
        Facts: []fact.Fact{{ Fact: fact.FactEmail }},
        Expiry: time.Minute * 5,
        AllowedFor: time.Day * 10,
    })
    check(err)
    // At this point the user will be prompted with a confirmation box to 
    // allow access its email for the next 10 days.
    //
    // If we send the same request again, it will be automatically shared by the device
    // without user interaction.
    resp, err := client.FactService().Request(&fact.FactRequest{
        SelfID:      selfID,
        Description: "info",
        Facts: []fact.Fact{{ Fact: fact.FactEmail }},
        Expiry: time.Minute * 5,
    })
    check(err)
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let tenDays = 10 * 60 * 60 * 60

    // Request email, with recurrent requests enabled for ten days
    let res = await sdk.facts().request(user, [{ fact: 'email_address', allowed_for: tenDays }])
    // At this point the user will be prompted with a confirmation box to 
    // allow access its email for the next 10 days.
    //
    // If we send the same request again, it will be automatically shared by the device
    // without user interaction.
    let res = await sdk.facts().request(user, [{ fact: 'email_address' }])
    {{% /tab %}}
{{% /tabs %}}

Given the user is always able to cancel this recurrent requests at any time, it's highly recommended to include the `allowed for` modifier on every request.

{{< notice note >}}Even the responses to your fact requests are automated by the user, have in mind the request always hits the user's device, so the response can take some time to get back to you..{{</ notice >}}

