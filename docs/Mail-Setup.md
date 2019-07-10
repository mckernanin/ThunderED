---
id: mail-setup
title: Mail Feed
---

Mail feed utilize the ESI API which require user responsible for feeding to authenticate in a special manner at least once before being able to supply mail. In order to setup this feed please follow the guide.

1. Setup **mailModule** section in **settings.json** file and add at least one group to **authGroups** section.

- **Id** - EVE character ID list to fetch mail from. You must login under this character in step #4.
- **Filters** - list of essential filters for incoming mail. Each filter can process mail by label, sender ID or mail list name. Also each filter has **FeedChannel** property to redirect filtered output into specified Discord channel.
- **DefaultChannel** - default Discord channel ID to feed your mail

2. Enable at least these modules in **config** section:

- "moduleWebServer": true
- "moduleMail": true

3. Goto web server main page (**!web** Discord command) and press **Mail Auth** button
4. Auth on the CCP web site under the authorized character.
5. That's all. At this point the bot will get ESI refresh token and will use it to fetch mail.

Note: If feeder wants to stop feeding mail he should remove the bot access rights from EVE account settings [here](https://community.eveonline.com/support/third-party-applications).
