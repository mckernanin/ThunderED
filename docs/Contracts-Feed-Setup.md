---
id: contracts-feed-setup
title: Contracts Feed Setup
---

### **Updated according to bot version 1.3.8**

**WARNING: Due to CCP restrictions citadel names can only be resolved if the feeding character or his corporation is added to the citadel ACL (access list).**

General rules to follow:

- Character IDs should be unique betweeen the groups as contracts are parsed once per character
- Prefer using Filters over creating new Groups for best performance
- Filters are **additive** meaning that contracts will fall under filter when all filtering conditions are met
- Enable at least **moduleWebServer** and **ModuleContractNotifications** modules to enable contract feeding

## Features

### Redirect contract messages to different users

You can set `"RedirectByIdInDescription": true` in a filter to enable bot to parse contract description text for Discord ID. For example if contract title is ID or ends with ID like `327501446738083843` or `Example desc text 327501446738083843` then bot will get it and try to find corresponding Discord user. If user has been found he will receive private message with contract feed.

if you want to also post redirected message to default contract feed channel set `"PostToChannelIfRedirected": true`.

### Simplified message stream

Set `"ShowOnlyBasicDetails": true` to display messages in a short format including Issuer, Recepient, Contract Type and Status.
![](http://joxi.ru/VrwV9Lgf7oK4oA.jpg)

### Click in Discord - open in game client

Set `"ShowIngameOpen": true` to display a clickable link in the contract message. When you click it you will have to authenticate under the character you want contract to be displayed for. This process won't store any data or ESI permissions and will grant single-use-only permission to open contract window in game client.
