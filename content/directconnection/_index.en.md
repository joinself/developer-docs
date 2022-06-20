---
title: "App direct connection"
date: 2022-02-15T11:02:05+06:00
icon: "ti-plug"
description: "App direct connection"
type : "docs"
keywords: ["connection", "connect", "qr"]
weight: 10
---

With this feature you'll be able to allow users to connect with your app offline (through a QR code or a dynamic link). 

In addition to a regular connection, you'll receive a callback notification once a user is connected with your app, which means you can use that callback as an entry point to build your business logic, like sending a welcome message.

Let's see an example for building this feature

### Generating a QR code

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    # Generates a QR code for the connection request
    @app.chat
        .generate_connection_qr
        .as_png(border: 0, size: 400)
        .save('/tmp/qr.png', :interlace => true)

    {{% /tab %}}

    {{% tab "Go" %}}
	qrdata, _ := s.chat.GenerateConnectionQR(chat.ConnectionConfig{
		Expiry: time.Minute * 5,
	})
    {{% /tab %}}

    {{% tab "Typescript" %}}
    // Generates a QR code for the connection request
    let buf = sdk.chat().generateConnectionQR()

    const fs = require('fs').promises;
    await fs.writeFile('/tmp/qr.png', buf);
    {{% /tab %}}
{{% /tabs %}}

<br />

### Generating a dynamic link

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    link = @app.chat.generate_connection_deep_link("")
    {{% /tab %}}

    {{% tab "Go" %}}
	link, err := s.chat.GenerateConnectionDeepLink(chat.ConnectionConfig{
		Expiry: time.Minute * 5, // this is required ?
	})
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let link = sdk.chat().generateConnectionDeepLink("")
    {{% /tab %}}
{{% /tabs %}}


### Subscribing to new connections

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    # Register an observer for a connection response
    @app.chat.on_connection do |res|
        if res.status == "accepted"
            p "successfully connected"
            @app.chat.message(res.from, "Hey there! We're connected!")
        end
    end
    {{% /tab %}}

    {{% tab "Go" %}}
	s.chat.OnConnection(func(iss, status string) {
		log.Println("Response received from " + iss + " with status " + status)
		parts := strings.Split(iss, ":")
		s.chat.Message([]string{parts[0]}, "Hi there!")
	})
    {{% /tab %}}

    {{% tab "Typescript" %}}
    sdk.chat().onConnection((res: any): any => {
      sdk.logger.info(`connection request ${res.status} by ${res.data.display_name}(${res.iss})`)
      sdk.chat().message(res.iss, "hi there!")
      exit()
    })
    {{% /tab %}}
{{% /tabs %}}