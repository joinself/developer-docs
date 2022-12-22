---
title: "Voice Calls"
date: 2022-02-15T11:02:05+06:00
icon: "ti-headphone-alt"
description: "Interact with voice call negotiation between users."
type : "docs"
keywords: ["voice"]
weight: 11
---

The Voice library is a subset of helpers to allow your app to act as proxy between two connected users.

Voice call negotiation at self follow a workflow like this:

- *start* starting messages instruct an identity to start a call with the issuer of the message using the same cid.
- *accept* the voice call has been accepted by the recipient, who responds with the details to start the voice call.
- *busy* notifies call issuer the recipient is busy and cannot answer the call.
- *stop* notifies the call has been ended by one of the users.

### SDK helpers

SDKs provide helpers to subscribe and send all voice negotiation messages, so you can build things like a calling proxy.
Let's see an example on how you could build a proxy.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @voice = client.Voice()
    @voice.on_start do |issuer, payload|
        call = Call.find_by(cid: payload[:cid])
        customer = call.connection
        operator = call.user
        puts "[voice_proxy] received start from #{issuer}, redirecting..."
        @voice.start customer.selfid,
                     payload[:cid],
                     payload[:call_id],
                     payload[:peer_info],
                     { operator_name: operator.name }

        end

        @voice.on_accept do |issuer, payload|
            call = Call.find_by(cid: payload[:cid])
            next if call.nil?

            customer = call.connection
            operator = call.user

            puts "[voice_proxy] received acceptation from #{issuer}, redirecting..."
            @voice.accept operator.selfid, 
                          payload[:cid], 
                          payload[:call_id], 
                          payload[:peer_info]
        end

        @voice.on_stop do |issuer, payload|
            call = Call.find_by(cid: payload[:cid])
            next if call.nil?

            customer = call.connection
            operator = call.user

            if issuer == operator.selfid
                puts "[voice_proxy] received stop from #{issuer}, redirecting to operator"
                @voice.stop customer.selfid, payload[:cid], payload[:call_id]
            else
                puts "[voice_proxy] received stop from #{issuer}, redirecting to customer"
                @voice.stop operator.selfid, payload[:cid], payload[:call_id]
            end
        end

        @voice.on_busy do |issuer, payload|
            call = Call.find_by(cid: payload[:cid])
            next if call.nil?

            customer = call.connection
            operator = call.user

            puts "[voice_proxy] received busy from #{issuer}, redirecting..."
            if issuer == operator.selfid
                @voice.busy customer.selfid, payload[:cid], payload[:call_id]
            else
                @voice.busy operator.selfid, payload[:cid], payload[:call_id]
            end
        end
    {{% /tab %}}

    {{% tab "Go" %}}
	voice := client.Voice()
    operator := "1112223334"
    customer := "1111111111"

        voice.OnStart(func(iss, cid, callID, peerInfo string, data interface{}){
            voice.Start(customer, cid, callID, peerInfo, map[string]string{
                "operator_name": "Bob",
            })
        })

        voice.OnAccept(func(iss, cid, callID, peerInfo string, data interface{}){
            voice.Accept(operator, cid, callID, peerInfo, map[string]interface{})
        })

        voice.OnStop(func(iss, cid, callID string) {
            if iss == operator {
                voice.Stop(customer, cid, callID)
            } else {
                voice.Stop(operator, cid, callID)
            }
        })

        voice.OnBusy(func(iss, cid, callID string) {
            if iss == operator {
                voice.Busy(customer, cid, callID)
            } else {
                voice.Busy(operator, cid, callID)
            }
        })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let voice = client.Voice()
    let operator = "1112223334"
    let customer = "1111111111"
        voice.onStart((iss: string, cid: string, call_id: string, peer_info: string, data: any) => {
            voice.start(customer, cid, call_id, peer_info, {
                "operator_name": "Bob",
            })
        })

        voice.onAccept((iss: string, cid: string, call_id: string, peer_info: string, data: any) => {
            voice.accept(operator, cid, call_id, peer_info, data)
        })


        voice.onStop((iss: string, cid: string, call_id: string) => {
            if (iss == operator) {
                voice.stop(customer, cid, call_id)
            } else {
                voice.stop(operator, cid, call_id)
            }
        })

        voice.onBusy((iss: string, cid: string, call_id: string) => {
            if (iss == operator) {
                voice.busy(customer, cid, call_id)
            } else {
                voice.busy(operator, cid, call_id)
            }
        })
    {{% /tab %}}
{{% /tabs %}}
