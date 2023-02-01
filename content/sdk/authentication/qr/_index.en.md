---
title: "QR"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 4
draft: false
# search related keywords
keywords: [""]
custom_title: "Authentication QR<div class='subtitle'>Authentication workflow through QR codes</div>"
toc: true
---

Presenting users with a QR makes your authentication workflow more convenient for users on non-mobile devices.

The authentication workflow using QR codes allows users to authenticate on your project without handwriting its self identifier, just by scanning the QR code you're providing.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
      # Generate a QR code to authenticate
      @app.authentication
          .generate_qr
          .as_png(border: 0, size: 400)
          .save('/tmp/qr.png', :interlace => true)
    {{% /tab %}}

    {{% tab "Go" %}}
	qrdata, err := s.auth.GenerateQRCode(&authentication.QRAuthenticationRequest{
		QRConfig: fact.QRConfig{
			Size:            400,
			BackgroundColor: "#FFFFFF",
			ForegroundColor: "#000000",
		},
	})
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let buf = sdk.authentication().generateQR()
    const fs = require('fs').promises;
    await fs.writeFile('/tmp/qr.png', buf);
    {{% /tab %}}
{{% /tabs %}}

Once the user scans the QR code with its device and accepts the authentication request, it will send back an authentication response to your app.

{{< notice note >}}Have in mind the user's device will send you back an authentication response, so [setup a subscription]({{< relref "/sdk/authentication/response/#subscribe" >}}) to that topic.{{</ notice >}}
