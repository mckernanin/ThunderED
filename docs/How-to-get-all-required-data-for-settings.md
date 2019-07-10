---
id: get-required-data
title: How to get all required data for settings
---

## Introduction

This guide also covers one important thing: how to correctly bind your Discord, CCP app and Bot together.
In short:

- Create Discord group and remember its GuildID (will be put into settings.json)
- Create Discord bot on their web site, add it to your Discord group. Remember TOKEN (will be put into settings.json)
- Create CCP app on their web site and remember **Client ID** and **Secret Key** (will be put into settings.json)

Read below for the detailed explanation.

## Discord IDs

### Channel and guild identifiers

**NEW METHOD**

1. Enable Developer Mode on Desktop Client: https://discordia.me/developer-mode
2. Right click on any channel or group icon and select **Copy ID** to copy the ID into clipboard. Then you can paste it into config.

General method:

1. Go to [Discord web site](https://discordapp.com/) and login into your group (or create new one)
2. Enter required channel
3. Look at the URL in your browser. For example: https://discordapp.com/channels/415097131124160779/415097964180847113

where

- 415097131124160779 - your guild ID (will be put into settings.json)
- 415097964180847113 - your current channel ID

Switch between your channels to get their IDs from URL.

### Bot ID

1. Go to [settings](https://discordapp.com/developers/applications/me/create) and create new bot
2. Remember **TOKEN** value on a BOT page in the menu (will be put into settings.json)

![](http://joxi.ru/p27W3GMhK0vYj2.jpg)

3. Get Cient ID

![](http://joxi.ru/12MWN8Ghl4nQWr.jpg)

4. Add Discord bot to you group using this link: https://discordapp.com/oauth2/authorize?&client_id=YOUR_BOT_CLIENT_ID&scope=bot&permissions=0 . Replace **YOUR_BOT_CLIENT_ID** by your Discord app client ID.

5. **IMPORTANT!** Assign Discord role to the bot inside your group with the privileges to change roles, names, etc. (preferably Admin). Make sure this role is **on top** of the common member roles in the Discord group role settings window. The order of roles in the Discord settings window **is important**! Roles can't mess with the roles which are on top of them.

## CCP IDs

### Developer Application

1. Go to [CCP website](https://developers.eveonline.com/applications)
2. Login with your account
3. Add new application

- Select **Authentication & API Access** connection type
- Select required ESI permissions. Note that it is adviced to select **everything** as these permissions don't expose anything on their own and just means that your app is allowed to work with them.
- Enter callback url identical to the external IP and Port in settings.json file like: `http://127.0.0.1:3000/callback` . Don't forget to strictly specify `callback` file endpoint. You can do it later when you setup your bot instance and find out what external address/port you will use.

4. Remember **Client ID** and **Secret Key** from apps main page (will be put into settings.json)

## EVE IDs

### Character, System, Region, Corporation or Alliance ID

1. Goto [Zkillboard.com](http://www.zkillboard.com)
2. Find required character, corp, alliance, region or system and look at the browser URL. For example: https://zkillboard.com/alliance/99004333/
   where 99004333 is your ID

**Note**: if character/corp has no ZKB profile search it on http://www.evewho.com and click ZKB link from there. You will be redirected on empty ZKB page but will have valid ID in URL anyway.

Go to [Configure settings.json](https://github.com/panthernet/ThunderED/wiki/Configure-settings.json)
