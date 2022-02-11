---
title: "Blocking fact request"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 1
draft: false
# search related keywords
keywords: ["fact", "facts", "request", "requests", "name", "email", "blocking"]
---

Same as with authentication there are situations where you want to block your execution line until the user responds to your **fact** request. For example, you may want to block a user's access to a certain space of your site until you verify its passport number.

This function blocks the execution line until the user responds with its verified email address.


{{% tabs groupId="install" %}}
    {{% tab "Ruby" %}}
        def get_email(selfid)
            res = @client.facts.request(selfid, [:email_address])
            return "" unless res.accepted?
            res.attestation_values_for(:email_address).first
            // Refer to Receiving fact response - Deal with request for more info
        rescue => e // An exception will be raised in case of a timeout or internal error
            return ""
        end
    {{% /tab %}}

    {{% tab "Go" %}}
    req := fact.FactRequest{
    SelfID:      selfID,
        Description: "info",
        Facts: []fact.Fact{{ Fact: fact.FactEmail }},
        Expiry: time.Minute * 5,
    }

    resp, err := client.FactService().Request(&req)
    if err != nil {
        return "", err
    }


    aa, err := resp.AttestaionValuesFor(fact.FactEmail)
    if err != nil {
        return "", err
    }

    println(aa[0])
    {{% /tab %}}

    {{% tab "Typescript" %}}
    try {
        let res = await sdk.facts().request(selfID, [{ fact: 'email_address' }])

        if (!res) {
            sdk.logger.warn(`fact request has timed out`)
        } else if (res.status === 'accepted') {
            let pn = res.attestationValuesFor('email_address')[0]
            sdk.logger.info(`${selfID} email address is "${pn}"`)
        } else {
            sdk.logger.warn(`${selfID} has rejected your authentication request`)
        }
    } catch (error) {
        sdk.logger.error(error.toString())
    }
    {{% /tab %}}
{{% /tabs %}}