---
id: message-templates-faq
title: Message templates FAQ
---

## Killmail Templates

### General

Default example template files are stored in **/Templates/Messages/default** folder with the **def.** prefix. They contain working templates you can use to start building your own.

Here are some basic rules you must follow in order to start using templated messages

1. Copy default template file into the /Templates/Messages directory. Linux users must copy them into preconfigured static data directory under the same folder structure: /Templates/Messages
2. Strip def. prefix from the file by renaming it into something like: **Template.killMailBig.txt**
3. There are three KM message types available: general, big and radius kills. Each have their own default template file to examine. EDIT: We now support custom templates for each feed group!
4. Lines started with // symbols are treated as comments and are ignored by processor.
5. Each default template file contains a set of variables you can use in your template. All of them are presented at the beggining of the file in commented lines. All variables must be specified within curved brackets, for ex. **{shipID}**.

### Syntax

Template syntax is very similar to Discord C# embed message form up. Processing starts with the EmbedBuilder line. All the consequent lines must start with the . symbol followed by command. **def.Template.killMailGeneral.txt** file contains pretty much every possible commands you can have in your template. All of the commands can have one or several arguments.
Template processor is very simple and fragile so do not try to insert or skip some symbols or whitespaces as it can ruin processing.

**Possible Arguments**

- Srict value written right inside: (0x0000ff)
- Text value set in the double apostrophe closing: ("Text message")
- No argument: ()

**Available line variations**

- .WithDescription("") - have one text argument. Description under the header.
- .WithThumbnailUrl("") - one text argument that must contain valid URL. Displays image on the right.
- .WithAuthor( - complex command that starts a series of subcommands and defines message header
  - .WithName("") - one text argument. Sets message header text.
  - .WithUrl("") - one text argument that must contain valid URL. Adds URL to the header.
  - .WithIconUrl("") - one text argument that must contain valid URL. Sets small Icon for the message.
- ) - specify this after the Author command series to close the sequence.
- .AddField("","") - two MANDATORY text arguments. Field header and body.
- .AddInlineField("","") - two MANDATORY text arguments. Inlined field header and body.
- .WithFooter("") - one text argument. Defines message footer with smaller text font.
- .WithImageUrl("") - one text argument that must contain valid URL.
- .WithTitle("") - one text argument.
- .WithTimestamp() - no arguments. Adds message timestamp to the bottom.

**How to handle variables**

Simple as ever! Just insert them inside the text argument body, for ex. "{victimName} is killed by {attackerName}".

**Conditional variables**

All variables that starts with _is_ are treated as conditional (Boolean) and can be used as simple condition to display different commands. For example lets take **{isLoss}** variable. We can write following string:
`#if {isLoss} .WithColor(0xff0000)`
This command will color our message frame in red ONLY when **{isLoss}** variable value will be TRUE meaning it is a loss KM. Next we can write another command with condition using the **!** symbol as logical NOT:
`#if !{isLoss} .WithColor(0x00ff00)`
This command will color our message frame in green when it is not a loss KM but kill actually.

So to summarize this: if line starts with **#if** followed by some **{variable}** it means that conseqent command will be processed or not processed based on variable value at the time of command execution.
