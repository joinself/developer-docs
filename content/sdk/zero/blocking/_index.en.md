---
title: "Blocking requests"
date: 2022-02-09T11:05:05+06:00
lastmod: 2022-02-09T11:05:05+06:00
weight: 1
draft: false
# search related keywords
keywords: ["fact", "anonymous", "zero knowledge", "zero", "intermediary", "blocking"]
---

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    facts = [{ sources: [SelfSDK::SOURCE_USER_SPECIFIED],
            fact: SelfSDK::FACT_EMAIL,
            operator: '==',
            expected_value: 'test@test.org' }]
    res = @client.facts.request_via_intermediary(selfid, facts)
    # GOTO Receiving fact response - Deal with the response
    {{% /tab %}}

    {{% tab "Go" %}}
    req := fact.IntermediaryFactRequest{
        SelfID:       selfID,
        Intermediary: intermediary,
        Description:  "info",
        Facts: []fact.Fact{
            {
                Fact:          fact.FactDateOfBirth,
                Sources:       []string{fact.SourceUserSpecified},
                Operator:      ">=",
                ExpectedValue: time.Now().Format(time.RFC3339),
            },
        },
        Expiry: time.Minute * 5,
    }

    resp, err := client.FactService().RequestViaIntermediary(&req)
    {{% /tab %}}

    {{% tab "Typescript" %}}
    try {
        let res = await sdk.facts().requestViaIntermediary(selfID, [{
            fact: 'unverified_phone_number',
            operator: '==',
            sources: ['user_specified'],
            expected_value: '+44111222333'
        }])
        if(!res) {
            sdk.logger.warn(`fact request has timed out`)
        } else if(res.status === "unauthorized") {
            sdk.logger.warn("you are unauthorized to run this action")
        } else if (res.status === 'accepted') {
            sdk.logger.info("your assertion is....")
            sdk.logger.info(res.attestationValuesFor('unverified_phone_number')[0])
        } else {
            sdk.logger.info("your request has been rejected")
        }
    } catch (error) {
        sdk.logger.error(error.toString())
    }
    {{% /tab %}}
{{% /tabs %}}