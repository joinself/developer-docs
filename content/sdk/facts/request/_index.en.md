---
title: "Request"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 1
draft: false
# search related keywords
keywords: [""]
custom_title: "Fact request<div class='subtitle'>Request users verified information</div>"
toc: true
---

### Blocking

Same as with authentication there are situations where you want to block your execution line until the user responds to your **fact** request. For example, you may want to block a user's access to a certain space of your site until you verify its passport number.

This function blocks the execution line until the user responds with its verified email address.

{{% tabs groupId="language" %}}
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
    resp, err := client.FactService().Request(&fact.FactRequest{
        SelfID:      selfID,
        Description: "info",
        Facts:       []fact.Fact{{ Fact: fact.FactEmail }},
        Expiry:     time.Minute * 5,
    })
    if err != nil {
        return "", err
    }
    aa, err := resp.AttestationValuesFor(fact.FactEmail)
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

### Non-blocking
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
    // Use goroutines to manage this scenario
    {{% /tab %}}

    {{% tab "Typescript" %}}
    // Use async() = {} to manage this scenario
    {{% /tab %}}
{{% /tabs %}}

### Asynchronous

The asynchronous approach can be used in scenarios like the previous one, however it has a subtle difference, you have a single observer for all information requests, which can be useful in some situations as you can have all the logic centralized on a single point.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    cid = @client.facts.request(selfid, [SelfSDK::FACT_EMAIL], async: true)
    {{% /tab %}}

    {{% tab "Go" %}}
    resp, err := client.FactService().RequestAsync(&fact.FactRequestAsync{
        SelfID:          selfID,
        Description: "info",
        Facts:       []fact.Fact{{ Fact: fact.FactEmail }},
        Expiry:      time.Minute * 5,
        CID:         "conversation_id",
    })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await sdk.facts().request(selfID, [{ fact: 'email_address' }], { async: true })
    {{% /tab %}}
{{% /tabs %}}