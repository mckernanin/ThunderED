---
id: notifications-setup
title: Notifications Feed
---

Notifications utilize the ESI API which require user responsible for feeding to authenticate in a special manner at least once before being able to supply notifications data. In order to setup notifications feed please follow this guide.

1. Setup **notifications** section in **settings.json** file. Read settings Wiki to know what to enter in each field.
2. Enable at least these modules in **config** section:

- "moduleWebServer": true
- "moduleNotificationFeed": true

2. Goto web server main page (**!web** Discord command) and press **Notifications Auth** button or enter **!authnotify** Discord command and follow the link.
3. Auth on the CCP web site under the authorized character.
4. That's all. At this point the bot will get ESI refresh token it will use to fetch notifications.

**WARNING: Due to CCP restrictions citadel names can only be resolved if the feeding character or his corporation is added to the citadel ACL (access list).**

Note: If feeder wants to stop feeding notifications he should remove the bot access rights from EVE account settings [here](https://community.eveonline.com/support/third-party-applications).
