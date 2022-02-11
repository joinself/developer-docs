---
title: "Blocking auth requests"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 1
draft: false
# search related keywords
keywords: [""]
---

This approach sends an authentication request and waits for the user to respond before continuing the execution.

This approach is useful when you want to wait for a user to respond to the authentication before continuing, and you don’t have timeout limitations on your server. An example could be authenticating a user on your command line script.

Lets see how it works, the functions below show a full cycle for a blocking authentication.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    begin
        @app.authentication.request("1112223334").accepted?
    rescue => e # An exception will be raised in case of a timeout or internal error
        return false
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    resp, err != client.AuthenticationService().Request("1112223334")
    if err != nil {
        println("authentication rejected")
        return
    }
    println(resp.Accepted)
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