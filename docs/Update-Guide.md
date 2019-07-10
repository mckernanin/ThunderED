---
id: update-guide
title: Update Guide
---

## Linux

Make sure you've set up static `Data` folder correctly as mentioned in [Installation Guide](https://github.com/panthernet/ThunderED/wiki/Build-&-Installation). This way you ensure that all sensitive data is untouched between software updates.

**TIP 1**: If you have customized language files consider specifying `"LanguageFilesFolder": "Data\Languages"` to store language files in static `Data` folder.

### Linux upgrade steps

1. Backup `Languages` folder where your ThunderED src is located if you don't follow **TIP 1** mentioned above.
2. Backup `edb.db` database file if you use SQLite DB (default).
3. Update source code. You have two options here.

-

1.  Download source code from Git if you use Docker: `git pull https://github.com/panthernet/ThunderED`
2.  Download [Latest Release](https://github.com/panthernet/ThunderED/releases) if you use Releases and unpack in the bot folder
3.  Update language files in your bot src or `Data` directory depending on where you store them. They're located in `Languages` sub-directory. Language files always contain new entries in the end of the files
4.  Update `settings.json` in `Data` directory. Read [Latest Release Notes](https://github.com/panthernet/ThunderED/blob/master/version.txt) for changes and look for new parameters.
5.  Build from source code if you use Docker: `docker build -t thundered .` or skip this step if you use Releases.
6.  Run the bot.

## Windows

### Windows upgrade steps

1. Backup `Languages` folder where your ThunderED installation is located if you don't follow **TIP 1** mentioned above.
2. Backup `edb.db` database file if you use SQLite DB (default).
3. Download [Latest Release](https://github.com/panthernet/ThunderED/releases) and unpack in the bot folder
4. Update language files in your bot installation directory or `LanguageFilesFolder` directory depending on where you store them. They're located in `Languages` sub-directory. Language files always contain new entries in the end of the files
5. Update `settings.json`. Read [Latest Release Notes](https://github.com/panthernet/ThunderED/blob/master/version.txt) for changes and look for new parameters.
6. Run the bot.
