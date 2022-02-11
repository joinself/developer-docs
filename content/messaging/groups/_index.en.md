---
title: "Group management"
date: 2022-02-09T11:05:05+06:00
lastmod: 2022-02-09T11:05:05+06:00
weight: 3
draft: false
# search related keywords
keywords: ["messaging", "message", "messages", "attachments", "read", "delivered", "edit", "delete", "remove"]
---

Managing group conversations is something really simple with Self SDK, let's see an end to end example to understand how they work.

{{% tabs groupId="install" %}}
    {{% tab "Ruby" %}}
    @groups = {}
    @app.chat.on_invite do |group|
        @groups[group.gid] = group
        group.join
        group.message("hi")
    end
    @app.chat.on_join do |msg|
        @groups[msg[:gid]].members << msg[:iss]
    end
    @app.chat.on_leave do |msg|
        @groups[msg[:gid]].members.delete(msg[:iss])
    end
    @app.chat.on_message do |msg|
        return if msg.gid.nil?
        puts "[#{@groups[msg.gid].name}] #{msg.from}: #{msg.body}"
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    groups := make(map[string]*chat.Group, 0)
	chat.ChatService().OnInvite(func(g *chat.Group) {
		g.Join()
		groups[g.GID] = g
		g.Message("hey!")
	})
	cs.OnLeave(func(iss, gid string) {
		delete(groups, gid)
	})
	chat.ChatService().OnJoin(func(iss, gid string) {
		if _, ok := groups[gid]; ok {
			groups[gid].Members = append(groups[gid].Members, iss)
		}
	})    
    chat.ChatService().OnMessage(func(cm *chat.Message) {
        if len(cm.GID) == 0 {
            return
        }
        fmt.Printf("[%s] %s: %s", groups[cm.GID].Name, cm.Iss, cm.Body) 
    })

    {{% /tab %}}

    {{% tab "Typescript" %}}
    let groups = {}
    sdk.chat().onInvite(async (g: ChatGroup) => {
      g.join()
      groups[g.gid] = g
      await groups[g.gid].message("hey!")
    })
    sdk.chat().onJoin(async (iss: string, gid: string) => {
      groups[gid].members.push(iss)
    })
    sdk.chat().onLeave(async (iss: string, gid: string) => {
      delete groups[gid].members[iss]
    })
    sdk.chat().OnMessage(async (cm: ChatMessage) => {
        if (len(cm.gid) > 0) {
            console.log(`[${groups[cm.gid].name}] ${cm.iss}: ${cm.body}`)
        }
    })
    {{% /tab %}}
{{% /tabs %}}

As you can see this example manages every group incoming message, to keep an in memory updated list of groups with its members. 

### Creating a group

Your app is als also able to create a group by calling invite method.
{{% tabs groupId="install" %}}
    {{% tab "Ruby" %}}
    members = [user1, user2, user3]
    @app.chat.invite "my_gid", "Group name", members
    {{% /tab %}}

    {{% tab "Go" %}}
    members = []string{user1, user2, user3}
    client.ChatService().Invite("my_gid", "Group name", members)
    {{% /tab %}}

    {{% tab "Typescript" %}}
    let members = [user1, user2, user3]
    sdk.chat().Invite("my_gid", "Group name", members)
    {{% /tab %}}
{{% /tabs %}}

{{< notice note >}}Have in mind you can send messages to a newly created group, but those messages will only be delivered to the group members that have decided to join the group.{{</ notice >}}

Groups can also have an image as avatar, you can pass a file contents as parameter to chat invite to provide that image.
{{% tabs groupId="install" %}}
    {{% tab "Ruby" %}}
    members = [user1, user2, user3]
    URI.open("https://www.avasflowers.net/img/prod_img/avasflowers-dreaming-of-tuscany-bouquet.jpg") do |image|
        @groups[gid] = @app.chat.invite(gid, "MagicGroup", members, { data: image.read, mime: "image/jpg" })
    end
    {{% /tab %}}

    {{% tab "Go" %}}
    members = []string{user1, user2, user3}
    data, err := os.ReadFile("/tmp/dat")
    check(err)
    client.ChatService().Invite("my_gid", "Group name", members, chat.InviteOptions{
        Data: data,
        Mime: "image.gif",
    })
    {{% /tab %}}

    {{% tab "Typescript" %}}
    import * as fs from 'fs';
    let data = fs.readFileSync('foo.txt','utf8');
    let members = [user1, user2, user3]
    sdk.chat().Invite("my_gid", "Group name", members, {
        "data": data, 
        "mime": "image/gif",
    })
    {{% /tab %}}
{{% /tabs %}}


### Messaging and groups

Sending messages to a group is as easy as calling the `message` method on that group. Additionally once you receive a message on a group you will have access to all its helpers to continue the conversation without having to care about the group itself.
