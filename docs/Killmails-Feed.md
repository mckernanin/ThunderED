---
id: killmails-feed
title: Killmail feed setup
---

# LiveKillFeedModule

To feed Abyssal loss KMs from the environment set `ShipEntities` to `[47465]`.
To feed all abyssal KMs set `LocationEntities` to `[12000001,12000002,12000003,12000004,12000005]`

- `StopOnFirstGroupMatch` - do not process KM in other groups if it has been successfuly processed in any of them. Setting it to `false` will transfer KM to the next group for processing (if any).

## Groups

Most of the `Group` params should be self explanatory but let's highlight some of them.

- `StopOnFirstFilterMatch` - do not process KM in other filters within a group if it has been successfuly processed in any of them. Setting it to `false` will transfer KM to the next group for processing (if any exist and `StopOnFirstGroupMatch` is false).
- `MessageTemplateFileName` - leave empty to use default or specify name of the file (ex. `template.txt`) from the `Data/Templates/Messages` folder (`Templates/Messages` on Windows).

## Filters

**WARNING!** Adding leading `-` sign to any entity name or ID will mark it as `excluded`. This will allow to filter out specific entities (systems, corps, types etc.) For example `"LocationEntities": ["-Jita"],` list should allow any system except `Jita` in `Inclusive` mode.

- `Inclusive` - filters can be inclusive or exlusive. The former will require KM to match specified criteria while the latter will require KM to not match it.
- `AllMustMatch` - Do not affect `exclusive` filters. If set to `true` then KM must match all criteria specified otherwise just any. Do not affect `Radius` system kills, only region and constellation.
- `ShipEntities` - list of victim ship types which can contain both ID and Name. Example: `"ShipEntities": [2323, "Ibis", "Sotiyo"]`
- `VictimEntities` - list of members which are the victims in KM. Can contain both ID and Name but require special prefixes for alliance and corporation names/tickers. Example: `"VictimEntities": ["-a:Snuffed Out", "c:Perkone", "Tau AD", 93045950]`
- `AttackerEntities` - list of members which are the attackers in KM. Can contain both ID and Name but require special prefixes for alliance and corporation names/tickers. Example: `"VictimEntities": ["-a:Snuffed Out", "c:Perkone", "Tau AD", -93045950]`
- `LocationEntities` - list of locations where KM can be generated. Can contain both ID and Name of system, constellation or region. No special prefixes required. Example: `"LocationEntities": ["Jita", "Black Rise", 30005304]`
- `Radius` - Default value is 0. Filter is treated as `radius` when it is greater than 0. Every system in `LocationEntities` will be a subject to radius calculations. Constellations and regions will be ignored.
- `DiscordChannels` - empty by default. Will override group `DiscordChannels` value and redirect KM feed for a filter when specified.
