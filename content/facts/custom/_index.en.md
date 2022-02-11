---
title: "Modifiers for fact requests"
date: 2018-12-29T11:02:05+06:00
lastmod: 2020-01-05T10:42:26+06:00
weight: 4
draft: false
# search related keywords
keywords: ["fact", "facts", "request", "requests", "name", "email", "modifiers", "options"]
---

A fact request accepts some modifiers for example

### CID

Passing the cid or conversation id, you'll be able to modify the default random uuid for that request, and easily identify the related response.


### exp_timeout

Timeout in seconds after which the request will expire. Useful if you want your **fact request** to be valid just for a specific period of time. It **defaults to 900 seconds**.
