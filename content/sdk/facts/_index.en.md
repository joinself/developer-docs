---
title: "Facts"
date: 2022-02-15T11:02:05+06:00
icon: "ti-files"
description: "Request access to a user's verified data"
type : "product"
weight: 4
---

A **Facts** is a statement about an **identity**. **Verified facts** are **facts** that have been **attested** to by trusted **issuer**(s).

A single **fact** can be **verified** by multiple issuers and so have multiple **assertions**. **Verified facts** are held by **identities** and  can be shared with other **identities (relying parties)** who require them.

Facts and related attestations are stored on the user’s device, so the user has full control over who can access its information.

Each fact has the following properties:

### Sources

A fact’s source represents where this fact comes from, for example a DOB can come from different sources such as a passport or a driving license. By default this field is set with a wildcard _“*”_ and the user will select the source on their device. Same happens if you specify multiple sources.

At the moment there are three different sources _user_specified_, _passport_ and _driving_license_.

As this list is always growing, you can check the possible values on your SDK [ruby-sdk](https://github.com/joinself/self-ruby-sdk/blob/master/lib/sources.rb#L6) and [go-sdk](https://github.com/joinself/self-go-sdk/blob/a027b7567d6d7d74ad2bbbf7219a24c57742b839/fact/fact.go#L20).

### Fact

This is the name of the fact you want to request like _display_name_, _email_address_ or _unverified_phone_number_.

The list of values by source is:

*   **_user_specified_**: _display_name_, _email_address_ and _unverified_phone_number_
*   **_passport_** and **_identity-card _**: _document_number_, _surname_, _given_names_, _date_of_birth_, _date_of_expiration_, _sex_, _nationality_, _country_of_issuance.
*   **_driving_license_** : _document_number_, _surname_, _given_names_, _date_of_birth_, _date_of_issuance_, _date_of_expiration_, _address_, _issuing_authority_, _place_of_birth_, _country_of_issuance_.

### Attestations

A list of **verified** **attestations** signed by an **issuer**. This only has content on _fact request_ responses, and it contains a list of **attestations** for the current fact.

### Expected value

When you send an **intermediary** fact check you expect the value of a user’s fact to be compared with an expected value, this field is where you will provide that value.

### Operator

On an intermediary fact check this field contains the operator used to compare the expected value against the expected value. Valid operators can be found [here](https://github.com/joinself/self-ruby-sdk/blob/master/lib/sources.rb#L34)



### Fact requests
**Fact** requests allow your app to request specific **facts** from identities on the _Self-network_.

Only **verified facts** can be requested

The approaches to request facts are similar to authentication, so let's have a look at them.

<aside class="success">
By default fact requests will expire after 15 minutes, you can change this defaults with `Expiry` option.
</aside>

