---
title: "Fact response"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 7
draft: false
# search related keywords
keywords: ["fact", "facts", "request", "requests", "name", "email", "response"]
---

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