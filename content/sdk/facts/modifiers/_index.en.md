---
title: "Modifiers"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 2
draft: false
# search related keywords
keywords: ["fact", "facts", "request", "requests", "name", "email", "modifiers", "options"]
custom_title: "Fact request modifiers<div class='subtitle'>Explore the different options a fact request sdk offers</div>"
toc: true
---

A fact request accepts some modifiers for example

### CID

Passing the cid or conversation id, you'll be able to modify the default random uuid for that request, and easily identify the related response.


### exp_timeout

Timeout in seconds after which the request will expire. Useful if you want your **fact request** to be valid just for a specific period of time. It **defaults to 900 seconds**.

### allowed_for

Providing this option with a number of seconds, your app will be allowed to request the same data without user confirmation for the specified time. 

This is quite useful if you intend to use some data recurrently but don't want to store it on your end.

Note this option is not compatible with `auth` modifier for security reasons.

### auth

Boolean representing if you want to display this fact request as an authentication with facts or not, it will default to false.