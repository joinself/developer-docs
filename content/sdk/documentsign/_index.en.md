---
title: "Document signing"
date: 2022-02-15T11:02:05+06:00
icon: "ti-check-box"
description: "Request and manage digital signatures"
type : "product"
keywords: ["document", "sign", "signature"]
weight: 9
toc: true
beta: true
---

Self allows you to request and manage digital signatures.

For example, you may need a user to digitally sign to indicate their agreement to your terms and conditions.

### Plain text signatures

Sometimes, a short text is enough, so you don't need to share a PDF to be signed; in those cases, you can send a document signature request as illustrated by the example below:

{{% tabs groupId="language" %}}
    {{% tab "Ruby" %}}
    @app.docs.request_signature ARGV[0], terms, [] do |resp|
        puts "Document signature : #{resp.status}"
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    res := client.DocsService().RequestSignature(os.Args[1], terms, []documents.InputObjects)
    log.Println(res)
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let resp = await sdk.docs().requestSignature(selfID, terms, [])
    console.log(`Document signature : ${resp["status"]}`)
    {{% /tab %}}
{{% /tabs %}}

<br />

### Object based signatures

If you need users to sign a blob (like a PDF) you can attach objects to your request, and your response will contain a list of signed objects.

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
	ds := client.DocsService()
	content, err := ioutil.ReadFile("./sample.pdf")
	if err != nil {
		log.Fatal(err)
	}    
	objects := make([]documents.InputObject, 0)
	objects = append(objects, documents.InputObject{
		Name: "Terms and conditions",
		Data: content,
		Mime: "application/pdf",
	})

	log.Println("sending document sign request")
	resp, err := ds.RequestSignature(os.Args[1], "Read and sign this documents", objects)
	if err != nil {
		log.Println(err.Error())
	}
	if resp.Status == "accepted" {
		fmt.Println("Document has been signed")
		fmt.Println("")
		fmt.Println("signed documents:")
		spew.Dump(resp.SignedObjects)
		for _, o := range resp.SignedObjects {
			fmt.Println("- Name: " + o.Name)
			fmt.Println("  Link: " + o.Link)
			fmt.Println("  Hash: " + o.Hash)
		}
		fmt.Println("")
		fmt.Println("full signature:")
		fmt.Println(resp.Signature)
	}
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let resp = await sdk.docs().requestSignature(selfID, terms, docs)
    if (resp["status"] == "accepted") {
      console.log("Document signed!")
      console.log("")
      console.log("signned documents: ")
      for (var i=0; i < resp["signed_objects"].length; i++) {
        console.log(`- Name : ${resp["signed_objects"]["name"]}`)
        console.log(`  Link : ${resp["signed_objects"]["link"]}`)
        console.log(`  Hash : ${resp["signed_objects"]["hash"]}`)
      }
      console.log("")
      console.log("full signature")
      console.log(resp["input"])
    }
    {{% /tab %}}
{{% /tabs %}}

The signed response will contain a SHA256 hash of the original blob, so you can verify the document has been signed.

