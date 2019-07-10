---
id: overview
title: Overview
---

ThunderED has multiple attachable modules which can be switched on and off. Each of these modules provide the very own functionality and benefits. The following overview will tell you about the most notable features this bot has to offer.

## Authentication

Auth is the cornerstone of this utility! You can control who is allowed into your Discord group, which roles they will receive and how they will be authenticated.
Features:

- Request ESI permissions from your members which will give you access to their skills, mail, transactions, contracts, etc.
- Discord roles will be automatically stripped when member leaves configured corp/alliance.
- Receive notifications about registrations and strips in specified Discord channel
- Use one button for several authentication rules
- Enforce names and corp/alliance tickers
- Bind alts to main characters

Related options in config file:

```
    "moduleWebServer": true, //core web server for all web-related modules (webServerModule section)
    "moduleAuthWeb": true, //provides authentication possibilities (WebAuthModule section)
    "moduleAuthCheck": true, //runs authentication checks to be able to strip roles from members
```

### [---> Read an extended FAQ for auth details <---](https://github.com/panthernet/ThunderED/wiki/Advanced-Web-Auth-and-JackKnife-utility)

![Web Auth Page](http://joxi.ru/1A55agNCD4EEBA.jpg)

## Live Kill Feeds from ZKB

Use common or radius live kill feed based on customized filters to display killmails you want. Track big kills, pve, pve or solo kills.

Features:

- Feed kills into several channels by different criterias
- Feed radius kills by # of jumps, constellation or region
- Customize KM messages using agile templates system

### [---> Read more about KM templates <---](https://github.com/panthernet/ThunderED/wiki/Message-templates-FAQ)

![KM example](http://joxi.ru/52a5ZOqCElxnd2.jpg)
