---
title: "Setup"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Setup your Self app"
type : "docs"
weight: 1
---

### Install the library
#### Android
Add the following to gradle dependencies block
{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}      
    implementation("com.joinself:mobile-sdk:1.0.0")    
    {{% /tab %}}    
{{% /tabs %}}


#### iOS
Add the following to `Pod` file
{{% tabs groupId="language" %}}
    {{% tab "Swift" %}}      
    pod 'SelfMobileSDK'
    {{% /tab %}}    
{{% /tabs %}}
