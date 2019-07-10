---
id: eve-chat-relay
title: EVE Chat Relay to Discord channels
---

### Introduction

**IMPORTANT**: There is no reliable way to access ingame chat channel messages except reading client log files. This makes the task of message relay very complex and (more important) unreliable. So treat this feature as a nice fancy addition to play with. Also, where is **NO** way you can legaly write messages to EVE chats outside the game itself and ThunderED will not support features which are against the game EULA.

Keep in mind the following notes:

- To relay messages you have to run **TED_ChatRelay** console app on a machine (or several machines) with running EVE Online client to be able to parse and transmit new chat messages.
- The transmition process has very basic security so be aware when you share your **relay codes** to other people who provide message feed

### Setup

1. Configure ThunderED settings. Enable **moduleWebServer** and **moduleChatRelay** modules in **config** section and add some relays to **chatRelayModule** section. Set EVE ingame channel name, Discord channel ID and pick some unique **relay code**.
2. Send **TED_ChatRelay** app to users who will feed EVE chat messages. They will require to add and configure **settings.json** file:

- **eveChannelName** - EVE ingame channel name equal to one in the bot relay settings
- **endpoint** - endpoint for ThunderED API with http://IP:PORT/chatrelay.php format
- **code** - code from step #1 equal to one in the bot settings

3. When user will run an app it will monitor file changes in the logs folder and transmit new messages to ThunderED bot endpoint.
