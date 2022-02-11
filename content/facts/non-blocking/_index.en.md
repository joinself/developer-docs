---
title: "Non-blocking fact request"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 1
draft: false
# search related keywords
keywords: ["fact", "facts", "request", "requests", "name", "email", "non-blocking"]
---
The sdk also allows us to send a fact request without blocking the execution line.

Same registration example we used for authentication works here, if you want to get a user **verified fact** but you don’t want the user to be blocked on the registration form, you can use this approach to continue with the execution line, and process the response as soon as it gets back.

Let’s see how we can request a verified email address with a non-blocking request.


{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
        def get_email_in_background(selfid)
            @client.facts.request(user, [:email_address]) do |res|
                return "" unless res.accepted?
                return res.attestation_values_for(:email_address).first
                # Refer to Receiving fact response - Deal with request for more info
            end
            rescue => e # An exception will be raised in case of a timeout or internal error
            return ""
        end
    {{% /tab %}}

    {{% tab "Go" %}}
    // Use goroutines to build a non-blocking example based on the blocking one
    go func() {
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

    if err != nil {
        // failed
    }
    // do something with email
    }
    {{% /tab %}}

    {{% tab "Typescript" %}}
    async() => {
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
    }
    {{% /tab %}}
{{% /tabs %}}