---
title: "Dealing with responses"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 7
draft: false
# search related keywords
keywords: [""]
---

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    if resp.accepted?
        p "accepted"
    elsif resp.rejected?
        p "rejected"
    elsif resp.unauthorized?
        p "unauthorized"
    elsif resp.errored?
        p "errored"
    else
        p "unkonwn status"
    end

    // Or simply access the status string
    p resp.status
    {{% /tab %}}

    {{% tab "Go" %}}
    // Go SDK will return an error for unsuccessful
    // responses
    err = authService.Request("1112223334")
    if err != nil {
        log.Fatal("auth returned with: ", err)
    }

    log.Println("authentication succeeded")
    {{% /tab %}}

    {{% tab "Typescript" %}}
    try {
    let res = await client.authentication().request("1112223334")
    if(res.isAccepted() == true) {
        client.logger.info(`${res.selfID} is now authenticated 🤘`)
    } else if(res.accepted == false) {
        client.logger.warn(`${res.selfID} has rejected your authentication request`)
    } else {
        client.logger.error(res.errorMessage)
    }
    } catch (error) {
        client.logger.error(error.toString())
    }
    {{% /tab %}}
{{% /tabs %}}

The interesting field in an authentication response is **status**. Valid values for status are:

##### accepted

The user has accepted the authentication request, so you can proceed authenticating it on your app.


##### rejected

The user has rejected the authentication request.


##### unauthorized

You’re unauthorized to interact with this user, let it know it needs to be connected to your app before continuing with an authentication process.


##### errored

An internal error happened.

Depending on the SDK there are different ways you can deal with different status, see some examples below

