---
title: "Authentication"
date: 2022-02-15T11:02:05+06:00
icon: "ti-lock"
description: "Biometric & Multi-factor authentication"
type : "product"
weight: 3
custom_title: "Authentication<div class='subtitle'>Multi-Factor and Biometric Authentication</div>"
toc: true
---

Self provides an easy to implement **Multi-factor and Biometric Authentication System**, which ensures a higher level of security for your applications. 
The Self Authentication System allows for seamless integration of biometric authentication without the need for passwords or codes, verifying users directly from their phones.

### Features

Biometric authentication: Verifies users through unique biometric identifiers, such as fingerprints or facial recognition.

Privacy-focused: Authenticates users by their Self Identifier without storing any other personal information.

Easy integration: Simple implementation of authentication workflow using the Self SDKs.


### Workflow

1. A user enters their Self Identifier (ID) within your application.
2. Your application requests authentication using the user's ID.
3. The user receives an authentication request on their phone, which may require biometric verification (e.g., fingerprint or facial recognition).
4. If the user successfully accepts the authentication request you'll be able to grant the current user

### Implementation Example

The following example demonstrates how to implement an authentication workflow using the Self Ruby SDKs.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    user = "1112223334"
    authenticated = @app.authentication.request(user).accepted?
    {{% /tab %}}

    {{% tab "Go" %}}
    user := "1112223334"
    if resp, err != client.AuthenticationService().Request(user); err != nil {
        println("authentication rejected")
        return
    }
    authenticated := resp.Accepted
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let res = await client.authentication().request("1112223334")
    let authenticated = res.isAccepted()
    {{% /tab %}}
{{% /tabs %}}

##### Steps to Implement the Authentication System
1. Integrate the Self SDKs into your application.
2. Allow users to enter their Self Identifier (ID) within your application.
3. Request authentication by calling the authentication.request() method, passing the user's ID as an argument.
4. Check if the authentication is accepted by evaluating the accepted? method.

### Benefits

**Enhanced security:** Multi-factor and biometric authentication provides an additional layer of security for your applications, making it more difficult for unauthorized users to gain access.

**Improved user experience:** Users no longer need to remember complex passwords or codes, as authentication is handled through Self identifiers.

**Privacy-focused:** The system verifies users by their ID without storing any other personal information, reducing the risk of data breaches.

### Conclusion

The Multi-Factor and Biometric Authentication System offers an effective and secure way to authenticate users for your applications. 

By implementing this system, you can offer your users a more convenient and secure authentication experience, while also protecting their privacy.
