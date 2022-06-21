---
title: "Custom facts"
date: 2022-02-15T11:02:05+06:00
date: 2022-02-15T11:02:05+06:00
weight: 8
draft: false
keywords: ["fact", "facts", "request", "requests", "custom"]
---

Self Core Facts are useful for general purpose, but the process of adding new core facts is slow and not flexible enough to support app custom facts.

Custom facts will allow you to:
 - Create custom facts.
 - Store facts on the user's device.
 - Consume custom facts.
 - Share custom facts with other apps.
 - Interact with other apps on the Self ecosystem.

All this is basically accomplished by using the user's device as secure storage for critical information.


 
### Issuing facts

#### Groups

Facts are presented to the user in groups. Groups have `name` and `icon` properties. 

| param  	| description  	| required  	|
|---	|---	|---	|
| name  	| The name of the group as it will be displayed to the user.  	| true  	|
| icon  	| The icon to be displayed close to the group name   	| false  	|

{{< notice note >}}Self App supports all material UI icons, you can search all available icons on [google fonts](https://fonts.google.com/icons?selected=Material+Icons&icon.query=plane).{{</ notice >}}

This is how we can create a group.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    my_group = SelfSDK::Services::Facts::Group.new(
        "Trip to Venice", 
        "airplanemode_active"
    )
    {{% /tab %}}

    {{% tab "Go" %}}
    {{% /tab %}}

    {{% tab "Typescript" %}}
    {{% /tab %}}
{{% /tabs %}}



#### Facts

Facts are composed of a key, a value and a source. 

| param  	| description  	| required  	|
|---	|---	|---	|
| key  	| is the id for the fact, it will allow other apps to request your facts by id.  	| true  	|
| value  	| It's stored as a string by default   	| true  	|
| source  	| it groups facts from the same source, it allows other apps to use it as filters.  	| true  	|
| group  	| if group is not provided facts will end under on the `ungrouped` section on the user's device  	| false  	|
| type  	| it defines how the fact has to be processed by other clients, it defaults to `string`, but can also be set as `password` or `delegation_certificate`  	| false  	|


- 

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    my_fact = SelfSDK::Services::Facts::Fact.new(
        "confirmation_code",
        "CD128763",
        "source12",
        group: my_group)
    {{% /tab %}}

    {{% tab "Go" %}}
    {{% /tab %}}

    {{% tab "Typescript" %}}
    {{% /tab %}}
{{% /tabs %}}



#### Issuing facts

Once you have your fact defined, it's time to send it to your user's device. You can do this by calling `issue` method on the facts service.

| param  	| description  	| required  	|
|---	|---	|---	|
| user  	| the user you're signing and sending facts to  	| true  	|
| facts  	| an array with the facts you want to issue   	| true  	|
| viewers  	| an array of app identifiers related to apps apps that can consume this facts   	| false  	|

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @app.facts.issue(user, 
                     my_fact], 
                     viewers: [appID1, appID2])
    {{% /tab %}}

    {{% tab "Go" %}}
    {{% /tab %}}

    {{% tab "Typescript" %}}
    {{% /tab %}}
{{% /tabs %}}


#### Retrieving facts

Retrieving facts is pretty much the same as we do for accessing core facts, the only difference is we must specify what issuers are we going to be accepting on our request, let's see an example.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    myAppID = ENV["SELF_APP_ID"]
    @app.facts.request(user, 
                       [{ 
                           fact: my_fact.key, 
                           issuers: [myAppID] 
                        }]) do |res|
        if res.status == "rejected"
            puts 'Information request rejected'
            exit!
        end
        k = my_fact.key.to_sym
        a = res.attestation_values_for(k)
        puts "Your stored fact is #{a.first}!"
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    {{% /tab %}}

    {{% tab "Typescript" %}}
    {{% /tab %}}
{{% /tabs %}}

#### Scope and facts

Custom facts scope is configurable by the developer by using `viewers` and `issuers` parameters to `facts.issue` and `facts.request`. This makes it possible to create private, protected and public custom facts.

##### Private

By specifying yourself as the only `viewers` on a facts.issue you will be creating facts you're the only one able to consume.

##### Protected

Specifying multiple app ids as `viewers` you'll make those facts available only to a subset of apps.

##### Public

When viewers parameter is not provided, issued facts become public.
