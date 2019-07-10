---
id: configure-settings
title: Configure settings.json
---

### Updated according to bot version 1.3.4

**HEY THERE!** We have a **CONFIG EDITOR** for this job. It might not be the best thing ever but will help you to understand settings and avoid errors. Tooltips and validation at hand! Check the latest bot release for a zip file.

Okay the most difficult part of the setup is correct settings configuration. Here is the breakdown of all the settings with the REQUIRED mark meaning the setting must be filled with correct value before you start the bot or corresponding module.

[Check this page](https://github.com/panthernet/ThunderED/wiki/How-to-get-all-required-data-for-settings) to find out how to obtain all required IDs.

### SOME BASIC RULES

- Group names must be unique within one host list
- Use https://jsonformatter.org/ to validate your config in case you've made a mistake while editing
- All parameters deleted from the file will be set to default values automatically. Feel free to clean up your config file if you wish. Though consider leaving vital params filled with correct values.
- **NEW!!!** Entities list params - accepts both names and numeric ID values. If these params are responsible for authentication you must specify prefixes for corp and alliance names like: "c: Corporation Name" and "a:Alliance Names". Character names are processed when no prefix is specified. You can distinct these fields in FAQ by **ENT** marks.

### "config" section

Contains general bot settings

- **botDiscordToken** - (REQUIRED) Discord bot token value
- **botDiscordName** - (REQUIRED) the name of the bot to display in Discord
- **botDiscordGame** - this string will be displayed in Discord under the bots name
- **botDiscordCommandPrefix** - (REQUIRED) single symbol which will represent bot command
- **discordGuildId** - (REQUIRED) ID of your Discord group (guild)
- **discordAdminRoles** - (REQUIRED) specify all Discord roles with admin privilegies. Users with these roles will also be able to run bot commands which require admin privilegies.
- **comForbiddenChannels** - the list of numeric channel IDs in which bot commands will be ignored
- **language** - interface and message language. Supported values: "ru-ru" and "en-us". Note that console text and logs will always be in english. You can add your own translation files in Languages directory.
- **useEnglishESIOnly** - specifies if queries and results from ESI should be received only in english or using the **language** settings.

- **moduleWebServer** - enable core web server, some modules depends on it. Disable if you don't use any web-related modules.
- **moduleAuthCheck** - enable auth check module which checks all authenticated users and strips roles if user has left your corp or alliance.
- **moduleAuthWeb** - enable web authentication module which allows specified corp or alle members to join your Discord group
- **moduleCharCorp** - enable char and corp query module (!char and !corp commands)
- **moduleReliableKillFeed** - enable reliable kills feed module based on ZKill API
- **moduleLiveKillFeed** - enable live kills feed module based on ZKill RedisQ
- **moduleRadiusKillFeed** - enable live radius kills feed around selected systems based on ZKill RedisQ
- **modulePriceCheck** - enable price check module (!pc, !jita etc. commands)
- **moduleTime** - enable eve time module (!time command)
- **moduleFleetup** - enable fleetUp module
- **moduleJabber** - enable jabber integration module
- **moduleMOTD** - (NOT IMPLEMENTED) enable channel MOTD module
- **moduleNotificationFeed** - enable notifications feed module
- **moduleStats** - enable !stat command module and auto-stats posting
- **moduleTimers** - enable web-timers module
- **moduleMail** - enable Mail feed module
- **moduleIRC** - enable IRC relay module
- **moduleTelegram** - enable Telegram relay module
- **moduleChatRelay** - enable EVE chat relay module
- **moduleIncursionNotify** - enable incursion notifications module
- **moduleNullsecCampaign** - enable nullsec entosis campaign notification module
- **moduleFWStats** - enable !fwstats command module
- **moduleLPStock** - enable module for LP queries (stats) and !lp commands
- **moduleHRM** - enable HRM module for character inspection that passed auth with ESI permissions
- **ModuleSystemLogFeeder** - enable bot internal log feed into specified Discord channel
- **ModuleContractNotifications** - enable module for contracts feed
- **ModuleSovTracker** - enable module for sov and ADM index changes feed

- **zkillLiveFeedRedisqID** - optional ZKill RedisQ queue name to fetch kills from. Could be any text value but make sure it is not simple and is quite unique. NOT USED if you use WebSockets mode.
- **timeFormat** - preferred time format
- **shortTimeFormat** - preferred short time format
- **dateFormat** - preferred date format
- **welcomeMessage** - display welcome message with authentication offer to all new users joining your Discord group hallway
- **cachePurgeInterval** - time interval in minutes to purge all outdated cache
- **memoryUsageLimitMb** - memory usage limit in Mb. If app reaches that limit it will try to free some memory.
- **logSeverity** - log all the app messages by specified severity and above (Values: Info, Error, Critical)
- **logNewNotifications** - TRUE by default. Will log all raw notifications data the bot fetches. This is needed to catch notifications which the bot could not yet process. Send me acquired data to add new notifications into bot.
- **requestRetries** - number of web-request retries before treating it as failed
- **extendedESILogging** - detailed ESI query logs
- **ESIAddress** - web address for ESI endpoint. Default: https://esi.evetech.net/
- **UseHTTPS** - (WIP) should allow work using https protocol. Might not work as expected.
- **RunAsServiceCompatibility** - forbids all console calls which can cause problems when bot is running as service
- **DisableLogIntoFiles** - disables log file generation with the exceptance of critical errors
- **UseSocketsForZKillboard** - use WebSockets for ZKill feeds which is way better than RedisQ mode. True by default.
- **ZKillboardWebSocketUrl** - ZKill webscokets url
- **LanguageFilesFolder** - custom language files folder

### "Database" section

- **databaseProvider** - (REQUIRED) database provider. Default value is **sqlite**. Values: sqlite, mysql
- **DatabaseFile** - the path to a database file for file-based DB. Default value is **edb.db**. Linux users are restricted to file name only while Windows users can set absolute and relative paths.
- **ServerAddress** - DB server address
- **ServerPort** - DB server port
- **DatabaseName** - DB schema or database name
- **UserId** - DB username
- **Password** - DB user password
- **CustomConnectionString** - (OPTIONAL) when this param is specified its value will be used as a connection string for a DB overriding all data specified above

### "ContractNotificationsModule" section

- **CheckIntervalInMinutes** - time interval to check for contract changes
- **MaxTrackingCount** - maximum number of recent contracts to keep track for. Default value is 150.
- **Groups** - feed groups
  - **GroupName** - each group must have unique name
    - **CharacterIDs** - list of numeric character IDs who will feed contract data
    - **ButtonText** - custom button text for web authentication as contract feeder
    - **DefaultMention** - default discord message mention. Default: @here
    - **FeedPersonalContracts** - this
    - **FeedCorporateContracts** - this
    - **Filters** - group filters collection
      - **FilterName** - filter names
        - **FeedIssuedBy** - include contracts issued by feeder
        - **FeedIssuedTo** - include contracts received by feeder
        - **Statuses** - list of allowed contract statuses. Values: "finished_issuer", "finished_contractor", "finished", "cancelled", "rejected", "failed", "deleted", "reversed", "in_progress", "outstanding"
        - **Availability** - list of allowed availability values. Values: "public", "personal", "corporation", "alliance"
        - **Types** - list of allowed contract types. Values: "unknown", "item_exchange", "auction", "courier", "loan"
        - **DiscordChannelId** - numeric Discord channel ID to feed filtered data
        - **ShowIngameOpen** - boolean value to display url in Discord messages to open contract in game client

### "SystemLogFeederModule" section

- **DiscordChannelId** - numeric Discord channel ID
- **OnlyErrors** - display only critical and error messages

### "ContinousCheckModule" section

This module is responsible for different routines not included in other modules which can happen in a set time intervals.

- **EnableTQStatusPost** - enable TQ status posting into a Discord channel when it changes
- **TQStatusPostMention** - default Discord mention for messages
- **TQStatusPostChannels** - list of numeric Discord channel IDs to post messagess into

### "StatsModule" section

- **EnableStatsCommand** - enable !stats command
- **RatingModeChannelId** - numeric DIscord channel ID for rating posts. If set will auto-post daily rating in this channel with all groups marked by **IncludeInRating** param.
- **DailyStatsGroups** - groups for daily stats posts
  - **GroupName** - group name
    - **DailyStatsChannel** - numeric Discord channel ID to post message
    - **DailyStatsCorp** - numeric EVE corporation ID (exclusive with DailyStatsAlliance)
    - **DailyStatsAlliance** - numeric EVE alliance ID (exclusive with DailyStatsCorp)
    - **IncludeInRating** - include this group in rating info post

### "hrmModule" section

This module is responsinle for JackKnife information storage and inspection

- AccessList
  - accessList1
    - **UsersAccessList** - the list of EVE character IDs who have access to inspection module
    - **RolesAccessList** - the list of Discord roles who have access to inspection module
    - **AuthGroupNamesFilter** - filter visible members by their auth group name
    - **AuthAllianceIdFilter** - filter visible members by their alliance ID
    - **AuthCorporationIdFilter** - filter visible members by their corporation ID
    - **ApplyGroupFilterToAwaitingUsers** - applies group filtering to members awaiting auth
    - **IsAwaitingUsersVisible** - control visibility of awaiting auth members section
    - **IsDumpedUsersVisible** - control visibility of dumped members section
    - **IsAuthedUsersVisible** - control visibility of authed members section
    - **IsSpyUsersVisible** - control visibility of spy members section
    - **IsAltUsersVisible** - control visibility of alt members section
    - **CanSearchMail** - HR user can search mail
    - **CanKickUsers** - HR user can delete member auth
    - **CanMoveToSpies** - HR user can move dumped members to spies
    - **CanSearchMail** - HR user can search mail
    - **CanRestoreDumped** - HR user can restore dumped members
    - **CanInspectAuthedUsers** - HR user can inspect authed members
    - **CanInspectAwaitingUsers** - HR user can inspect awaiting members
    - **CanInspectDumpedUsers** - HR user can inspect dumped members
    - **CanInspectSpyUsers** - HR user can inspect spy members
    - **CanInspectAltUsers** - HR user can inspect alt members
- **AuthTimeoutInMinutes** - web session timeout value
- **TableEntriesPerPage** - default number of entries per inspection page
- **TableSkillEntriesPerPage** - number of character skills per page. Default: 20
- **UseDumpForMembers** - use dump section for members otherwise they will be deleted on the first kick request
- **DumpInvalidationInHours** - dumped members will be deleted from DB when these hours will pass. 0 value will disable clean up.
- **SpiesMailFeedChannelId** - enables mail feed from spies into specified channel. Default value is 0 - disabled.

### "mailModule" section

This module allows authenticated characters to feed their in-game mail into the specified Discord channels. Mail will be filtered by specified labels which you can create and assign to you mails in-game.

- **checkIntervalInMinutes** - interval in minutes to check for new mail
- **authGroups** - character groups allowed to auth as mail feeders
  - **group1** - group name
    - **id** - character ID
    - **includePrivateMail** - include private mail to this feed
    - **DefaultChannel** - numeric Discord channel ID to feed all mail by default
    - **DefaultMention** - default Discord mention to add to each mail
    - **Filters** - the list of specific mail filters
      - **filterName** - each name must be unique. All filter criterias are ADDITIVE.
        - **FilterLabels** - list of in game EVE mail label names which will be used to mark and fetch mails
        - **FilterSenders** - list of numeric 'FROM' character IDs to filter incoming mail
        - **FilterMailList** - list of EVE ingame maillist names
        - **FeedChannel** - numeric Discord channel ID to feed this mail. 0 to use default.

### "timersModule" section

This module brings Timers web-page with the SSO auth and filterable read/edit access rights. You can use it to log and receive notifications about important upcoming timers.

- **authTimeoutInMinutes** - web session timeout in minutes
- **autoAddTimerForReinforceNotifications** - automatically add timer event upon receiving structure reinforce notification (if notifications feed module is enabled)
- **TinyUrl** - optional short custom url MANUALLY generated by YOU and wrapping the possibly long timers auth url
- **grantEditRolesToDiscordAdmins** - auto grant editor roles to Discord admins based on the config section
- **announces** - list of numeric values representing the time in minutes to send timer reminder message to discord when specified amount of minutes is left before the timer ends
- **announceChannel** - Discord channel ID for announce messages
- **TimeInputFormat** - time format for input fields. Default: DD.MM.YYYY hh:mm
- **DefaultMention** - default Discord mention
- **accessList** - list of entities which has view access to the timers page
  - **group1** - group name
    - **FilterEntities** - (**ENT**) list of anmes and numeric ID values corresponding to character, corporation or alliance.
    - **FilterDiscordRoles** - list of text Discord role names
- **editList** - list of entities which has edit access on the timers page
  - **group1** - group name
    - **FilterEntities** - (**ENT**) list of anmes and numeric ID values corresponding to character, corporation or alliance.
    - **FilterDiscordRoles** - list of text Discord role names

### "CommandsConfig" section

Contains settings for various bot commands

- **EnableCapsCommand** - enable !caps command
- **CapsCommandDiscordRoles** - restrict !caps command to the following Discord roles. Empty by default, allowed to everyone.
- **CapsCommandDiscordChannels** - restrict !caps command to the following Discord channels. Empty by default, allowed everywhere.

### "webServerModule" section

Contains setings for the built-in web-server

- **discordUrl** - Discord group invitation url
- **ccpAppClientId** - (REQUIRED) text client ID from the CCP application
- **ccpAppSecret** - (REQUIRED) text client code from the CCP application
- **webExternalIP** - (REQUIRED) text **EXTERNAL IP** address or domian name of the server machine which is used to receive connections from the internet
- **webExternalPort** - (REQUIRED) numeric port value for external IP. Set the one which is not used by your OS and opened for interactions (like 8080).

### "radiusKillFeedModule" section

Contains settings for radiusKillFeedModule module. This module uses ZKill RedisQ to fetch live killmails as they're happening in EVE and filter it by specified radius around selected systems.

- **groupsConfig** - can have several feeds (groups) defined
  - **group1** - each group can have unique name which will be displayed in a message
    - **radius** - numeric value of number of jump around specified system. Leave 0 and specify radiusSystemId to limit feed by only one system.
    - **radiusChannel** - discord channel ID to post messages
    - **radiusSystemId** - numeric radius central system ID (even wormhole J system can be specified). You should specify only one of the following IDs: system, constellation or region.
    - **radiusConstellationId** - numeric constellation ID. Specifying this will feed KMs from entire constellation.
    - **radiusRegionId** - numeric region ID. Specifying this will feed KMs from entire region.
    - **minimumValue** - minimum ISK value to filter killmails
    - **FeedPvpKills** - process PVP kills in this group
    - **FeedPveKills** - process PVE kills in this group
    - **FeedUrlsOnly** - feed data using ZKB url which will automatically unfold in Discord. This is fastest but not customizable method.

### "liveKillFeedModule" section

Contains settings for liveKillFeed module. This module uses ZKill RedisQ to fetch live killmails as they're happening in EVE. If you want reliable KM feed only for your corp or ally please use reliableKillFeed module.

- **bigKill** - numeric value in ISK to consider the kill to be BIG enough
- **bigKillChannel** - numeric channel ID to post all GLOBAL big kills in EVE, 0 to skip
- **groupsConfig** - groups for KM filtering
  - **group1** - each group name should be UNIQUE
    - **name** - this name will be posted along the KM
    - **discordChannel** - (REQUIRED)numeric ID of the Discord channel to post KMs of this group into
    - **corpID** - (REQUIRED or use allianceID) numeric corporation ID. Specify to fetch all KMs for this corporation. Mutually exclusive with allianceID.
    - **allianceID** - (REQUIRED or use corpID) numeric alliance ID. Specify to fetch all KMs for this alliance. Mutually exclusive with corpID.
    - **minimumValue** - minimum KM ISK value
    - **minimumLossValue** - minimum loss KM ISK value. Set to very high value to disable losses.
    - **bigKillValue** - minimum KM ISK value to be considered as BIG for this group
    - **bigKillChannel** - post BIG KMs to separate channel. Numeric channel ID value.
    - **bigKillSendToGeneralToo** - also post big kills to the channel specified in **discordChannel** setting
    - **FeedPvpKills** - process PVP kills in this group
    - **FeedPveKills** - process PVE kills in this group
    - **FeedUrlsOnly** - feed data using ZKB url which will automatically unfold in Discord. This is fastest but not customizable method.

### "WebAuthModule" section - settings for authWeb and authCheck modules

This section contains settings for authentication process of _moduleAuthWeb_ and _moduleAuthCheck_ modules.

- **authCheckIntervalMinutes** - numeric time interval in minutes to run auth checks of existing users
- **StandingsRefreshIntervalInMinutes** - numeric time interval in minutes to run standings refresh for feeders
- **exemptDiscordRoles** - the list of Discord role names which will not be checked for authentication (admins etc.)
- **AuthCheckIgnoreRoles** - the list of Discord role names whih will be ignored during auth check
- **authReportChannel** - numeric ID of the channel to report bot auth actions. Preferably for admins only. Leave 0 to disable.
- **comAuthChannels** - (REQUIRED) the list of channels where !auth command is allowed
- **DefaultAuthGroup** - optional name of the auth group from AuthGroups list which will be used to generate auth url on
- **enforceCorpTickers** - automatically assign corp tickers to users
- **enforceAllianceTickers** - automatically assign alliance tickers to users
- **enforceCharName** - automatically assign character names to users (setup Discord group to disallow name change also)
  !auth command
- **UseOneAuthButton** - enable mode when only one auth button is displayed. In this case the bot will search available groups for authentication. If found auth group contains ESI permissions then user must be authenticated twice using automatic redirects so user logs in once and select character twice.
- **authGroups** - the list of groups to filter auth requests

  - **group1** - groups must have UNIQUE names

    - **AllowedCharacters** - list of corporations to check for auth
      - **charName** - each entry must have unique name
        - **Id** - numeric character ID
        - **DiscordRoles** - the list of Discord role names to assign upon successful check against this char
    - **AllowedCorporations** - list of corporations to check for auth
      - **corpName** - each entry must have unique name
        - **Id** - numeric corporation ID
        - **DiscordRoles** - the list of Discord role names to assign upon successful check against this corp
    - **AllowedAlliances** - list of alliances to check for auth
      - **alyName** - each entry must have unique name
        - **Id** - numeric alliance ID
        - **DiscordRoles** - the list of Discord role names to assign upon successful check against this alliance
    - **authRoles** - the list of Discord role names who can manually auth preliminary users
    - **ManualAssignmentRoles** - the list of Discord role names which can be manually assigned to user in Discord and which will be ignored by bot while user successfully passes auth check against this auth group. Will be stripped when user is no longer passing auth check.
    - **PreliminaryAuthMode** - enable this mode to be able to put applicants on hold after initial auth. They can be examined and accepted/declined later.
    - **AppInvalidationInHours** - number of hours to keep preliminary applications
    - **ESICustomAuthRoles** - the list of ESI permission names to fetch during auth
    - **CustomButtonText** - the text on a web button corresponding to this auth group
    - **DefaultMention** - default Discord mention upon successful auth
    - **SkipDiscordAuthPage** - skip Discord auth code but store ESI token for further examination
    - **UseStrictAuthenticationMode** - don't search for additional filters upon first auth filter match. When false (default) will search through all available filters within a group.
    - **ExcludeFromOneButtonMode** - when **UseOneAuthButton** mode is **true** this group will have separate auth button and will not be searched when registering using one-button mode.
    - **BindToMainCharacter** - when **true** enables this group to act as an alt binding group when user select already authed main character first and then auth with an alt. Alt characters are available for inspection in HR module.

    - **StandingsAuth** - enables [standing-based auth](https://github.com/panthernet/ThunderED/wiki/Advanced-Web-Auth-and-JackKnife-utility) when specified
      - **CharacterIDs** - list of numeric character IDs authorized to feed standings data
      - **WebAdminButtonText** - custm web buttton text for feeders authentication
      - **UseCharacterStandings** - this
      - **UseCorporationStandings** - this
      - **UseAllianceStandings** - this
      - **StandingFilters** - list of standing filters
        - **defaultFilter** - filter name
          - **Standings** - list of decimal or integer numbers corresponding to standing value
          - **Modifier** - modifier to apply. Values: eq, le, ge, lt, gt
          - **DiscordRoles** - discord role names to assign

### "resources" section

- This section defines some web resource URLs which the bot will use

### "notificationFeedModule" section - settings for notifications module

This module will feed authenticated character notifications into the specified Discord channels. Notifications could be filtered by type and redirected to different channels.

- **checkIntervalInMinutes** - time interval in minutes to run new notifications check. Due to natural delay in notifications on CCP side it is not wise to set it lower than 2 minutes.
- **groups** - the list of character keys which will be authorized to share their notifications
  - **groupName1** - group names must be UNIQUE. Database check depends on this name, please set only once for better experience.
    - **characterID** - numeric EVE character ID
    - **defaultDiscordChannelID** - numeric default Discord channel ID. All notifications filters will use this channel to send messages by default.
    - **fetchLastNotifDays** - numeric number of days to fetch old notifications for newly registered feeder. 0 by default meaning no old notifications will be feeded.
    - **filters** - the list of filters to sort incoming notifications.
      - **filter1** - UNIQUE filter name. Database check depends on this name, please set only once for better experience.
        - **DefaultMention** - default Discord mention command to use for this group
        - **channelID** - numeric Discord channel ID to redirect messages. Leave 0 to use group default channel.
        - **charMentions** - list of numeric EVE CHARACTER IDs to mention them in the message. Characters must be authed on the server for this to work thus allowing to get their Discord IDs. Leave empty to use **@everyone** mention.
        - **roleMentions** - list of Discord role names to mention. Role must be configured in Discord to be mentionable.
        - **notifications** - list of text notification types this filter has access to

Each entry represents EVE official notification type name and channel value defining where to send the message. Only notification types listed in the default settings file are supported.

### "fleetupModule" section

This module feeds FleetUp ops notifications into the specified channel.

- **UserId** - FleetUp API key user ID
- **APICode** - FleetUp API key code
- **AppKey** - FleetUp application key
- **GroupID** - FleetUp group ID
- **channel** - numeric Discord channel ID
- **announce_post** - announce newly posted opses in Discord channel
- **announce** - list of numeric values representing reminders in minutes before the ops start
- **DefaultMention** - default Discord mention
- **FinalTimeMention** - final timer announce mention

### "ircModule" section

This module relays messages between IRC and Discord channels

- **Server** - [REQUIRED] IRC server address
- **Port** - [REQUIRED] IRC server port
- **UseSSL** - use SSL connection
- **Password** - IRC user password
- **Nickname** - IRC nickname
- **Nickname2** - secondary IRC nickname in case the first one is in use
- **Username** - IRC username
- **Realname** - IRC real name
- **Invisible** - IRC visibility setting
- **AutoReconnect** - auto reconnect to IRC server on connection loss
- **AutoReconnectDelay** - delay in milliseconds
- **AutoRejoinOnKick** - auto rejoin channels on kick
- **QuitReason** - message to display on channel quit
- **ConnectCommands** - the list of IRC commands to perform upon successful chat login
- **RelayChannels** - groups of settings for message relay
  - **irc** - IRC channel name string prefixed with #
  - **discord** - Discord numeric channel ID
  - **discordFilters** - Discord messages that contain these strings will be filtered from relay
  - **discordFiltersStartsWith** - Discord messages that start with these strings will be filtered from relay
  - **ircFilters** - IRC messages that contain these strings will be filtered from relay
  - **ircFiltersStartsWith** - IRC messages that start with these strings will be filtered from relay
  - **relayFromDiscordBotOnly** - relay only ThunderED bot messages from specified Discord channel
  - **ircUsers** - relay messages only from specified IRC usernames

### "telegramModule" section

This module relays messages between Telegram and Discord channels

- **token** - Telegram bot token string
- **RelayChannels** - groups of settings for message relay
  - **telegram** - Telegram channel numeric ID
  - **discord** - Discord channel numeric ID
  - **discordFilters** - Discord messages that contain these strings will be filtered from relay
  - **discordFiltersStartsWith** - Discord messages that start with these strings will be filtered from relay
  - **telegramFilters** - Telegram messages that contain these strings will be filtered from relay
  - **telegramFiltersStartsWith** - Telegram messages that start with these strings will be filtered from relay
  - **relayFromDiscordBotOnly** - relay only ThunderED bot messages from specified Discord channel
  - **telegramUsers** - relay messages only from specified Telegram users. First check for Telegram @username then by First Name + Second Name.

### "chatRelayModule" section

This module receives chat messages from auxillary **TH_ChatRelay** application and posts them in a Discord channel.

- **RelayChannels** - list of channels to relay
  - **eveChannelName** - name of the EVE channel
  - **discordChannelId** - numeric Discord channel ID
  - **code** - unique string code to identify this relay block. You have to specify this code in TED_ChatRelay app settings too.

### "incursionNotificationModule" section

This module posts notifications about incursions right after the TQ downtime. Region and Const filters are additive.

- **DiscordChannelId** - numeric Discord channel ID
- **DefaultMention** - default Discord mention
- **Regions** - list of numeric region IDs to filter incursions
- **Constellations** - list of numeric constellation IDs to filter incursions
- **ReportIncursionStatusAfterDT** - set to **True** if you want bot to post status update about existing incursions. Set to **False** to report only new incursions.

### "nullsecCampaignModule" section

This module posts notifications about nullsec sovereignty campaigns in selected regions or constellations.

- **CheckIntervalInMinutes** - numeric interval in minutes to check for campaigns
- **Groups**
  - **groupName1** - **[SENSITIVE]** group name is used to store values in DB
    - **Regions** - list numeric EVE region IDs
    - **Constellations** - list of numeric EVE region IDs (additive to Regions)
    - **Announces** - list of numeric intervals im minutes for campaign notification announcement
    - **Mentions** - list of text Discord mentions to use for this group notifications
    - **DefaultMention** - default Discord mention to use
    - **ReportNewCampaign** - send notification message upon finding new campaign
    - **DiscordChannelId** - Discord numeric channel ID to post notifications
