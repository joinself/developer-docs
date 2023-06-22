---
title: "Initializing your client"
date: 2022-02-09T11:02:05+06:00
lastmod: 2022-02-09T11:02:05+06:00
weight: 3
draft: false
# search related keywords
keywords: ["install", "setup", "initialisation"]
---


### Install your client
{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    $ gem install "selfsdk"
    {{% /tab %}}

    {{% tab "Go" %}}
    $ go get github.com/joinself/self-go-sdk
    {{% /tab %}}

    {{% tab "Typescript" %}}
    $ npm install self-sdk
    {{% /tab %}}
{{% /tabs %}}

We currently offer support for some basic clients. We are always happy to receive contributions to review - send us a PR, or contact us at info@joinself.com to share what you have built with us!

Language | URL
--------- | -----------
Go | [https://github.com/joinself/self-go-sdk](https://github.com/joinself/self-go-sdk)
Ruby | [https://github.com/joinself/self-ruby-sdk/](https://github.com/joinself/self-ruby-sdk/)
Typescript | [https://github.com/joinself/self-typescript-sdk/](https://github.com/joinself/self-typescript-sdk/)


### Referencing the SDK

SelfSDK is referenced like any other library for each specific language.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    require "selfsdk"
    {{% /tab %}}

    {{% tab "Go" %}}
    import "github.com/joinself/self-go-sdk"
    {{% /tab %}}

    {{% tab "Typescript" %}}
    const SelfSDK = require("self-sdk");
    {{% /tab %}}
{{% /tabs %}}



### Storage key generation

Self-SDK locally persists session and account information needed for end to end encryption. A SELF_STORAGE_KEY is required to securely encrypt this information.
It is recommended that you use a large random string for your SELF_STORAGE_KEY. You can generate a random string through the command line with:

`$ LC_ALL=C tr -dc '[:alnum:]' < /dev/urandom | head -c64`

Keep that key in a secure place as you’ll need it to initialize a connection.


### Basic connection

A basic connection to _Self network_ only requires your _SELF_APP_ID_, _SELF_APP_DEVICE_SECRET_, _SELF_STORAGE_KEY_ and _SELF_STORAGE_DIR_.

You may want to add _SELF_APP_ID_, _SELF_APP_DEVICE_SECRET_, _SELF_STORAGE_KEY_ and _SELF_STORAGE_DIR_ as environment variables.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client = SelfSDK::App.new(ENV["SELF_APP_ID"], 
                               ENV["SELF_APP_DEVICE_SECRET"], 
                               ENV["SELF_STORAGE_KEY"], 
                               ENV["SELF_STORAGE_DIR"])
    {{% /tab %}}

    {{% tab "Go" %}}
    client, err := selfsdk.New(selfsdk.Config{
        SelfAppID:           os.Getenv("SELF_APP_ID"),
        SelfAppDeviceSecret: os.Getenv("SELF_APP_DEVICE_SECRET"),
        StorageKey:          os.Getenv("SELF_STORAGE_KEY"),
        StorageDir:          os.Getenv("SELF_STORAGE_DIR"),
    })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    const client = await SelfSDK.build( 
        os.Getenv("SELF_APP_ID"),
        os.Getenv("SELF_APP_DEVICE_SECRET"),
        os.Getenv("SELF_STORAGE_KEY"),
        os.Getenv("SELF_STORAGE_DIR"),
    {{% /tab %}}
{{% /tabs %}}



### Custom environment

When you’re debugging your app, you may want to point to the _sandbox environment_ instead of _production_ to run your tests. You can define the environment by passing additional parameters to the _Self client_ initialization.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client = SelfSDK::App.new(ENV["SELF_APP_ID"], 
                               ENV["SELF_APP_DEVICE_SECRET"], 
                               ENV["SELF_STORAGE_KEY"], 
                               ENV["SELF_STORAGE_DIR"],
                               env: :sandbox)
    {{% /tab %}}

    {{% tab "Go" %}}
    client, err := selfsdk.New(selfsdk.Config{
        SelfAppID:           os.Getenv("SELF_APP_ID"),
        SelfAppDeviceSecret: os.Getenv("SELF_APP_DEVICE_SECRET"),
        StorageKey:          os.Getenv("SELF_STORAGE_KEY"),
        StorageDir:          os.Getenv("SELF_STORAGE_DIR"),
        Environment:	     "sandbox",
    })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    const client = await SelfSDK.build( 
        os.Getenv("SELF_APP_ID"),
        os.Getenv("SELF_APP_DEVICE_SECRET"),
        os.Getenv("SELF_STORAGE_KEY"),
        os.Getenv("SELF_STORAGE_DIR"),
        { 'env': 'sandbox' })
    {{% /tab %}}
{{% /tabs %}}

### Reconnection

Self-SDK keeps a websocket connection open to self-messaging, but eventually, that connection may drop. By default _Self-SDK_ will try to reconnect, but you can override this behaviour by passing custom parameters to initialization.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @client = SelfSDK::App.new(ENV["SELF_APP_ID"], 
                               ENV["SELF_APP_DEVICE_SECRET"], 
                               ENV["SELF_STORAGE_KEY"], 
                               ENV["SELF_STORAGE_DIR"],
                               auto_reconnect: false)
    {{% /tab %}}

    {{% tab "Go" %}}
    client, err := selfsdk.New(selfsdk.Config{
        SelfAppID:           os.Getenv("SELF_APP_ID"),
        SelfAppDeviceSecret: os.Getenv("SELF_APP_DEVICE_SECRET"),
        StorageKey:          os.Getenv("SELF_STORAGE_KEY"),
        StorageDir:          os.Getenv("SELF_STORAGE_DIR"),
        ReconnectAttempts:	 -1,
    })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    const client = await SelfSDK.build( 
        os.Getenv("SELF_APP_ID"),
        os.Getenv("SELF_APP_DEVICE_SECRET"),
        os.Getenv("SELF_STORAGE_KEY"),
        os.Getenv("SELF_STORAGE_DIR"),
        { 'autoReconnect': false })
    {{% /tab %}}
{{% /tabs %}}


