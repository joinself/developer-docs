---
title: "Dynamic link"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 5
draft: false
# search related keywords
keywords: [""]
custom_title: "Authentication Dynamic link<div class='subtitle'>Authentication workflow through Dynamic links</div>"
toc: true
---

When you're authenticating users on your platform straight on their mobile devices, is when dynamic links are more useful. 

A dynamic link will authenticate a user on your platform by clicking a link and accepting the authentication request on his phone.

As part of this process, you have to share the generated link with your users, and wait for a response.

In order to use a dynamic link, you must generate a redirection code on the developer portal, once you have it you can use it to generate a url which you can share with your users.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
      url = @client.authentication.generate_deep_link(redirection_code)
    {{% /tab %}}

    {{% tab "Go" %}}
	link, err := authService.GenerateDeepLink(&authentication.DeepLinkAuthenticationRequest{
		ConversationID: cid,
		Callback:       redirectionCode,
		Expiry:         time.Minute * 5,
	})
	if err != nil {
		log.Fatal("auth returned with: ", err)
	}
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let url = sdk.authentication().generateDeepLink(redirectionCode)
    {{% /tab %}}
{{% /tabs %}}

{{< notice note >}}Have in mind the user's device will send you back an authentication response, so [setup a subscription]({{< relref "/sdk/authentication/response/#subscribe" >}}) to that topic.{{</ notice >}}
