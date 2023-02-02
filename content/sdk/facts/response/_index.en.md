---
title: "Response"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 3
draft: false
# search related keywords
keywords: ["fact", "facts", "request", "requests", "name", "email", "response"]
custom_title: "Processing fact response<div class='subtitle'>Manage responses and extract the verified facts</div>"
toc: true
---

### Subscribe

As the user also has the option to accept or reject a fact request, the response also comes with a status property and some helpers like the authentication response.

Additionally a fact response comes with a list of attestations for the requested fact.

Subscribing to a **facts** response is similar to authentication.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client.facts.subscribe do |resp|
        # GOTO Deal with the response for details
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    // TBD
    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.facts().subscribe((res: any): any => {
        // GOTO Deal with the response for details
    })
    {{% /tab %}}
{{% /tabs %}}

### Processing fact response

The fact response will comes with a status and the same list of helpers as we described on [authentication](/authentication/response/) to deal with it.

Additionally each fact of the response has a list of attestations let’s see how to process them.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    resp.facts.each do |fact|
        p fact.name
        fact.attestations do |a|
            p "received #{a.value} from #{a.source}/#{a.fact} signed by #{a.origin}"
        end
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    for _, f := range resp.Facts {
        log.Println(f.Fact, ":", f.AttestedValues())
    }

    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.logger.info(res.attestationValuesFor('phone_number')[0])
    {{% /tab %}}
{{% /tabs %}}