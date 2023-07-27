---
title: "SDK Reference"
date: 2022-02-15T11:02:05+06:00
font: "material"
icon: "rocket_launch"
description: "Self SDK reference"
type : "docs"
custom_title: "Self SDK reference<div class='subtitle'>Comprehensive reference for integrating with Self SDK</div>"
toc: true
---
Self SDKs are divided on different services, each service matches one of the products Self is offering.


<table class='reference'>
    <tbody>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "setup" >}}">Setup</a>
                </div>
                <div class='section_subtitle'>Setting up your client</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "setup/initialize" >}}">Initialize</a></li>
                    <li><a href="{{< relref "setup/disconnect" >}}">Disconnect</a></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "messaging" >}}">Messaging</a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "messaging/text-messages/" >}}">Send</a></li>
                    <li><a href="{{< relref "messaging/text-messages/" >}}">Receive</a></li>
                    <li><a href="{{< relref "messaging/actions/#mark-as-read" >}}">Mark as read</a></li>
                    <li><a href="{{< relref "messaging/actions/#mark-as-received" >}}">Mark as received</a></li>
                    <li><a href="{{< relref "messaging/actions/#edit" >}}">Edit</a></li>
                    <li><a href="{{< relref "messaging/actions/#delete" >}}">Delete</a></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "groups" >}}">Groups</a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "messaging#creating-a-group" >}}">Create</a></li>
                    <li><a href="{{< relref "messaging#messaging-and-groups" >}}">Messaging</a></li>
                    <li><i>Add users</i></li>
                    <li><i>Remove users</i></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "objects" >}}">Objects</a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "objects#public-objects" >}}">Attach a public object</a></li>
                    <li><a href="{{< relref "messaging#non-public-objects" >}}">Attach non public objects</a></li>
                    <li><i>Process incoming objects</i></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "documentsign" >}}">Document signature <span class="beta">beta</span></a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "documentsign#plain-text-signatures" >}}">Signing a plain text</a></li>
                    <li><a href="{{< relref "documentsign#object-based-signatures" >}}">Signing an object</a></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "authentication" >}}">Authentication</a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "authentication/request" >}}">Request</a></li>
                    <li><a href="{{< relref "authentication/modifiers/" >}}">Request modifiers</a></li>
                    <li><a href="{{< relref "authentication/response/" >}}">Response</a></li>
                    <li><a href="{{< relref "authentication/qr" >}}">QR</a></li>
                    <li><a href="{{< relref "authentication/dynamic_link" >}}">Dynamic Links</a></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "facts" >}}">Facts</a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "facts/request/" >}}">Request</a></li>
                    <li><a href="{{< relref "facts/modifiers" >}}">Request modifiers</a></li>
                    <li><a href="{{< relref "facts/response/" >}}">Response</a></li>
                    <li><a href="{{< relref "facts/custom/" >}}">Custom facts</a></li>
                    <li><a href="{{< relref "facts/recurrent/" >}}">Recurrent</a></li>
                    <li><a href="{{< relref "facts/combined/" >}}">Auth combination</a></li>
                    <li><a href="{{< relref "facts" >}}">QR</a></li>
                    <li><a href="{{< relref "facts" >}}">Dynamic Links</a></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "connections" >}}">Connections</a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "connections#permit-connections" >}}">Permit</a></li>
                    <li><a href="{{< relref "connections#revoke-specific-connection" >}}">Revoke</a></li>
                    <li><a href="{{< relref "connections#listing-connections" >}}">List</a></li>
                </ul>
            </td>
        </tr> 
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "voice" >}}">Voice Calls</a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "voice" >}}">Start</a></li>
                    <li><a href="{{< relref "voice" >}}">Accept</a></li>
                    <li><a href="{{< relref "voice" >}}">Busy</a></li>
                    <li><a href="{{< relref "voice" >}}">Stop</a></li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <div class="section_title">
                    <a href="{{< relref "directconnection" >}}">Connection</a>
                </div>
                <div class='section_subtitle'>Interacting with users through chat</div>
            </td>
            <td class="Row_contents__EJTwh">
                <ul>
                    <li><a href="{{< relref "directconnection#generating-a-qr-code" >}}">Generating a QR code</a></li>
                    <li><a href="{{< relref "directconnection#generating-a-dynamic-link" >}}">Generating a dynamic link</a></li>
                    <li><a href="{{< relref "directconnection#subscribing-to-new-connections" >}}">Subscribing to new connections</a></li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### SDK Access

To build an app on self-network its required to have our app installed so you can log in to the Self Developer Portal ([production](https://developer.joinself.com) or [sandbox](https://developer.sandbox.joinself.com)).


### SDK Host

When you start playing with Self you likely want to use  [Sandbox environment]({{< ref "quickstart/sandbox" >}}) environment, as it's easier to setup and less restrictive.

Please visit the  [Sandbox documentation page]({{< ref "quickstart/sandbox" >}}) to download our mobile client from app stores. 

### Platform status and incidents

Project status page is available at [status.joinself.com](https://status.joinself.com/)

### Client libraries

Self offers official SDK libraries for different programming languages, which are regularly updated for breaking and non-breaking changes.

<div class='clients_list'>

<table class='languages'>
    <tbody>
        <tr>
            <td width='60'><a href='https://github.com/joinself/self-ruby-sdk/' target='_blank'><img src="/images/ruby.png" alt="ruby" width="50"/></a></td>
            <td><a href='https://github.com/joinself/self-ruby-sdk/' target='_blank'>Ruby SDK</a></td>
        </tr>
        <tr>
            <td><a href='https://github.com/joinself/self-go-sdk/' target='_blank'><img src="/images/go.png" alt="ruby" width="50" style='padding-top:10px'/></a></td>
            <td><a href='https://github.com/joinself/self-go-sdk/' target='_blank'>GO SDK</a></td>
        </tr>
        <tr>
            <td><a href='https://github.com/joinself/self-typescript-sdk/' target='_blank'><img src="/images/typescript.png" alt="typescript" width="50"/></a></td>
            <td><a href='https://github.com/joinself/self-typescript-sdk/' target='_blank'>Typescript SDK</a></td>
        </tr>
        <tr>
            <td><a href='https://github.com/joinself/self-rust-sdk/' target='_blank'><img src="/images/rust.png" alt="ruby" width="50"/></a></td>
            <td><a href='https://github.com/joinself/self-rust-sdk/' target='_blank'>Rust SDK</a></td>
        </tr>
    </tbody>
</table>

</div>

### Self hosted HTTP service

In addition to the official SDKs we also provide a [self hosted HTTP Self service](https://github.com/joinself/restful-client) that allows you to interact with the Self Network through a Rest API.


