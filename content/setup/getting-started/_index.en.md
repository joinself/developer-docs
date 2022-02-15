---
title: "Getting started"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 2
draft: false
# search related keywords
keywords: ["setup", "configuration", "requirements"]
---

### Requirements

To build an app on self-network its required to have our app installed so you can log in to the [Self Developer Portal](http://developer.joinself.com/).

Please visit the official app stores to download our official apps for [Android](#) and [iOS](#)


### Create an account

Visit [Self Developer Portal](http://developer.joinself.com/) and follow the steps to register. You'll need a Self Identifier account to proceed.


###  App creation

*Self-apps* are autonomous self identities able to interact with other identities on the *Self-network*.

A developer can create an app through the developer portal. This app will be identified by a *SELF_APP_ID* and a *SELF_APP_DEVICE_SECRET*.

*SELF_APP_ID* is your public identifier on the network and you can share it with other peers. You must keep *SELF_APP_DEVICE_SECRET* in a secure place.

You’ll see below how to use these two strings to initialize your client and start interacting with the *Self-network*.

{{< notice note >}}Remember — copy and store *SELF_APP_DEVICE_SECRET*, as we don't have access to it.{{</ notice >}}

### Environments

Self provides a sandbox so you can try your app code before moving to production. You can register for a free developer account and create new test apps on the Sandbox developer portal [here](https://developer.sandbox.joinself.com).

Once your app is ready you can create a new one on production [here](https://developer.joinself.com)