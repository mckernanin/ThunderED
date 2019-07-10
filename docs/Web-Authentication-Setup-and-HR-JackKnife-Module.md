---
id: web-auth-setup
title: Web Authentication Setup and HR(JackKnife) module
---

**Updated for version 1.4.1**

### GUIDELINES

- REUQIREMENTS: Set up built-in web server, enabled and setup modules: `moduleWebServer`, `moduleAuthWeb`, `moduleAuthCheck`
- Authentication works within `WebAuthModule` and can be set up using the so called `groups` - list entries which you can setup to support different auth modes.
- Member filters for authentication are implemented using `Entities` logic: you can specify both IDs and names in one entities list. Note that alliance name/ticker should have `a:`prefix (`a:CONDI`) and corporation name/ticker should have `c:` prefix (`c:Starlane Limited`). Character name should be used without prefixes.
- You can remove all properties/modules which is left untouched from default config file to lessen config size. Their values will be filled with defaults like in the default config file.
- Sample config sections for all auth modes are available in the default settings file.
- We have **CONFIG EDITOR** tool to help with the configuration tuning. Get it with the latest release package.

### BASIC RULES

- Auth groups will be checked according to their order in config file: top to bottom. Independent of the auth type (general, standing, titles, etc.).
- Allowed members in auth groups will be checked from top to bottom with the following priority: character, corporation, alliance
- Guest groups should go last in the list or they will be chosen before latter groups
- Guest groups must have empty `Entities` list (no more 0)!
- `StopSearchingOnFirstMatch` now properly limits the search. If it is `false` when all members within a single group will be checked. This will allow to assign roles to user from multiple `AllowedMembers` entries form ONE group matching the criteria. If mentioned property is `true` then only the first matching entry will be used to grant roles. The same rules applies to standings auth.
- If user matches several criteria within the group and they contain `Titles`: only the 1st found entry with `Titles` auth will be selected and all other matches will be omitted

Following auth modes are covered within this article:

- MODE1: General auth with no special permissions
- MODE2: General auth with special ESI permissions request from applicant. Creates separate auth button on web server.
- MODE3: Preliminary auth with special ESI permissions request from applicant. Creates separate auth button on web server.
- MODE4: General or preliminary auth using character Standings system.
- MODE5: Guest mode with/without ESI permissions
- MODE6: Alt characters auth mode - bind alt chars to your main without Discord auth
- MODE7: Auth by corp titles
- SIMPLIFIED Auth Mode - fast and effective auth management
- GENERAL TIPS
- HR module setup

**NOTE**: Groups order matters! Auth check will run from top to bottom.

Scroll down to know more information.

### MODE1 - General Auth

In this mode no additional permissions are requested from applicants. It is simple and straightforward: applicant will be successfully authenticated if his char/corp/alliance matches any criteria specified in **AllowedMembers** list.

### MODE2 - General Auth with ESI permissions

Same as MODE1 with one notable change. Applicants will receive request during auth process to share ESI permissions specified in **ESICustomAuthRoles** param. Upon successful authentication bot will receive refresh token which will be used to get valid user access tokens from CCP to be able to query data limited by specified ESI permissions. Refresh tokens are stored in a database and can be invalidated by user at any time in EVE Online account settings on CCP web site.
**NOTE: You have to add all required ESI permissions to your CCP app before you can use them in auth process**

### MODE3 - Preliminary Auth

This mode is enabled when you set **PreliminaryAuthMode** param to `True` for the selected auth group. When this mode is activated it is possible for **any** applicant to pass initial auth. During this auth bot will get their ESI permissions and token as described in MODE2. Full authentication will occur automatically when user char/corp/alliance will match any criteria specified in **Allowedmembers** list. Otherwise this mode will force applicants to wait for an approval or invitation making it possible to inspect them using HR module before they're allowed into your corporation or alliance.

### MODE4 - Standings Auth

**WARNING**: It is recommended to have only one feeder to avoid confusion with possible standings conflicts though the bot will just check for the first condition matching its search criteria.

This mode uses different access check system based on EVE standings. It is enabled when you specify **StandingsAuth** param block which is **null** by default. Once set it will ignore **AllowedMembers** list and will search for standings information supplied by characters specified in **CharacterIDs** param. Standings feeders must complete separate auth process using the special button in auth section on web site. This mode can operate in both general and preliminary states supporting logic described in the previous modes.

Access checks are controlled by filters in **StandingFilters** param block. Available **Modifier** values:

- **eq** - standing EQUAL to specified value
- **lt** - standing LESS THAN specified value
- **gt** - standing GREATER THAN specified value
- **le** - standing LESS THAN OR EQUAL to specified value
- **ge** - standing GREATER THAN OR EQUAL to specified value

**WARNING**: Make sure filters do not overlap numeric standing values to avoid possible conflicts. The bot will process values in the following modifier order: **eq -> le -> ge -> lt -> gt**

### MODE5 - Guest Mode

To enable guest mode make single entry in **Allowedmembers** list and leave `Entities` list empty. This will allow any applicant to authorize. If you want to set special guest role for these users then you can specify roles in **DiscordRoles** list.

### MODE 6 - Alt characters authentication

Set **BindToMainCharacter** to **true** for a group with empty **AllowedMembers** list. This will force this group to act as an alt binding group which will have separate auth button and registration process.
In this mode you can bind alt characters with custom ESI permissions to the already authed main characters. Alt characters are dependant from the main character i.e. will be deleted if main character auth is deleted. They can be inspected in HR module and can be used by some Discord commands like !ships.

### MODE 7 - Auth by corp titles

Add entries to `Titles` list in the `AllowedMembers` group for this mode to activate. Look for `Mode7_AuthByTitles` in default config file.
Several rules:

- Titles auth is only enabled when `Titles` property within `AllowedMembers` group is not empty
- Auth group must fetch `esi-characters.read_titles.v1` ESI permission from users
- `DiscordRoles` property from `AllowedMembers` will be ignored
- Corp directors will not be authenticated as they don't have corp titles

### SIMPLIFIED Auth Mode

This is not a standalone auth mode but rather an extension to any auth group predefined in **settings.json** file. It allows you to simplify auth management process when you have to add/remove entities from auth groups a lot.

**NOTE**: We have web editor available for this feature in `WebConfigEditor` module.

Take a look at the **\_simplifiedAuth.def.txt** file which is supplied with the bot release. Rename it to **\_simplifiedAuth.txt** and place into the static data folder where your **settings.json** file reside.
Each entry in this file corresponds to separate corp/alliance declared by its name rather than ID. Let's take an example:
`Goonswarm Federation|GuestAuthGroup|GuestRole,TempRole`
All fields in an entry are `|` delimeted and Discord roles are comma delimited. Here is `Goonswarm Federation` stands for entity name, `GuestAuthGroup` is auth group name from your settings file and `GuestRole,TempRole` are Discord role names to assign upon successfull authentication.

All entries specified in this file will be automaticaly injected into existing auth groups upon bot startup/rehash. Basically you have to preconfigure auth groups in **settings.json** file once and use this file to effectively manage authentication process.

### General Tips!

- **DO NOT** rename auth groups in config file as it will invalidate authentication for members authed under these groups. If you want to change group name for some reason please refer to !rngroup command: run it, stop the bot, change group name inside the config file and run the bot again.
- Set **UseOneAuthButton** to **true** to enable one-button auth mode with only one auth button. If authenticating character matches a group with ESI permissions specified he will require to auth one more time to feed ESI permissions (automatically redirected). You can also set **ExcludeFromOneButtonMode** to **true** on a group level to exclude this group from one-button mode.
- If you want to have custom Discord roles which are not specified in auth groups and not assigned automatically then you have several params to do so:
  - **exemptDiscordRoles**: if member has a role from this list it will not pass authentication at all meaning that this role will persist even if he will leave your corp/alliance. Manage these roles with caution.
  - **ManualAssignmentRoles** are roles which can be assigned to authed members within an auth group and will persist until member authentication is failed (due to leaving corp/alliance). These roles will be stripped when auth check is failed for the assigned member.

## HR module setup

Considering the above you can build your own "JackKnife" recruitment process for selected group as following:

1. Create auth group with **PreliminaryAuthMode** set to **true**. This will force group to accept all auth requests and enable refresh token fetch if **ESICustomAuthRoles** is specified. All appllicants will be put on hold for consequent actions.
2. An applicant should confirm his registration in Discord using **!auth confirm CODE** command displayed during auth process. It is needed to bind EVE character to Discord account.

Now the applicant will be available for inspection in HR Module web page.
Decision:

- If you decide to accept applicant then just invite him to your corporation/alliance and the bot will automatically auth him in Discord based on **AllowedMembers** conditions list.
- If you decide to decline application you can set **AppInvalidationInHours** param which will delete applications when specified amount of hours has passed, decline them manually in HRM module or by using **!auth decline CODE/ID** command.

HR module also affects management process by introducing **UseDumpForMembers** param which will enable dumpster section for characters. Instead of being deleted when their auth fails (or manually) they will be put into dumpster - a temporary buffer which allows you to cancel the delete operation or move this character into SPIES section.

SPIES section is designated for characters that has left your corp/alliance and joined some other entity you're interested in spying on. The amount of the information available from them completely depends on the ESI permissions they had authed with before.

### **Note that even if ThunderED supports SPIES section its Author is not responsible for potential CCP EULA breach on the bot Client side which might be related to excessive spying using 3rd party tools. It is left up to you to inform your users that their ESI tokens will be stored in the database and can be invalidated by the users themselves.**
