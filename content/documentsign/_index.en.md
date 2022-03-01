---
title: "Document sign"
date: 2022-02-15T11:02:05+06:00
icon: "ti-check-box"
description: "Request document signatures"
type : "docs"
keywords: ["document", "sign", "signature"]
weight: 9
---

As an app developer you may want my users to provide signatures on specific texts or documents, and have proof they agree on those documents. 

Most common case is accepting your service terms and conditions.

### Plain text signatures

Sometimes a short text is enough, so you don't really need to share a PDF to be signed, in those cases you can send a document signature request like:

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @app.docs.request_signature ARGV[0], terms, [] do |resp|
        puts "Document signature : #{resp.status}"
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    // TBD
    {{% /tab %}}

    {{% tab "Typescript" %}}
    // TBD
    {{% /tab %}}
{{% /tabs %}}

<br />

### Object based signatures

In case you want users to sign a document (like a PDF) you can attach objects to your request, and get a list of signed objects on the response.

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    objects = []
    File.open('./sample.pdf') do |f|
        objects << {
            name: "Terms and conditions",
            data: f.read,
            mime: 'application/pdf'
        }
    end
    @app.docs.request_signature ARGV[0], terms, objects do |resp|
        if resp.status == 'accepted'
            puts "Document signed!".green
            puts ""
            puts "signed documents: "
            resp.signed_objects.each do |so|
                puts "- Name:  #{so[:name]}"
                puts "  Link:  #{so[:link]}"
                puts "  Hash:  #{so[:hash]}"
            end
            puts ""
            puts "full signature:"
            puts resp.input
        else
            puts "Document signature #{'rejected'.red}"
        end
        exit
    end
    # Check the full example on:
    # https://github.com/joinself/self-ruby-sdk/examples/document_sign/app.rb
    {{% /tab %}}

    {{% tab "Go" %}}
    // TBD
    {{% /tab %}}

    {{% tab "Typescript" %}}
    // TBD
    {{% /tab %}}
{{% /tabs %}}

As you can see the signed response will come with a SHA256 hash of the original document, so you can verify the document has been signed.

