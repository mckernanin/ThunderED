---
id: build-installation
title: Build & Installation
---

### Updated according to bot version 1.4.1

You can use precompiled version supplied with [app release on GitHub](https://github.com/panthernet/ThunderED/releases) which do not require any 3rd party software and can be run out of the box. You can also manually compile .NET core source code to self-sufficient application for many different platforms if you like.

The configuration file setup can be tricky but we have **config editor** app supplied with each release. Go to [How to get all required data for settings](https://github.com/panthernet/ThunderED/wiki/How-to-get-all-required-data-for-settings) page to find out what settings you have to set.

### Preparations

- Create Discord bot and CCP app. ([Look here for a guide.](https://github.com/panthernet/ThunderED/wiki/How-to-get-all-required-data-for-settings))
- Setup MySQL database (or skip it and use default SQLite out of the box)
  - Install and access MySQL server
  - Deploy **mysql.dump** provided with release or within source code root folder
  - Make sure that MySQL is allowed to receive external connections
  - Don't forget to setup **Database** config file section later

### Windows Installation Process

1. Obtain latest software distrib from the [Releases page](https://github.com/panthernet/ThunderED/releases) and skip to entry #5. If you want to build solution for target platform other than win10-x64 [please read this topic](https://blogs.msdn.microsoft.com/luisdem/2017/03/19/net-core-1-1-how-to-publish-a-self-contained-application/).

2. If you want to compile the source code you had to install Visual Studio 2017 with selected .NET Core dev components and then grab bot source code from the main page on the GitHub.
3. Open solution in VS and publish **ThunderED** project (win10-x64/Release by default)
4. Copy results from the **ThunderED\bin\Release\netcoreappX.X** folder to your designated server.

5. (Optional) Obtain static IP or domain name for your server or web authentication will not work as CCP app requires static callback address available from the internet to send auth data.
6. Create and setup **settings.json** config file based on the **settings.def.json** file included in the package. You can use **config editor** for this (mentioned above). [Read description of different config parameters](https://github.com/panthernet/ThunderED/wiki/Configure-settings.json)
7. Run ThunderED.exe

### Linux Installation Process

1. Install Docker for Linux. It will pull .NET Core from the image.

- Install Docker: `sh <(curl -fsSL get.docker.com)`
- Download docker-compose: `sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose`
- Make docker-compose executable: `chmod +x /usr/local/bin/docker-compose`

2. Build from source code or install pre-compiled version

- 2A. Get source code and prepare the package using the following commands as an example:
  - Download source code from Git: `git clone https://github.com/panthernet/ThunderED`
  - Go to your bot folder: `cd ThunderED/ThunderED`
  - Create settingsfile from default `cp settings.def.json settings.json` and edit it to your needs (or use Windows config editor and copy result file into Linux). [Read description of different config parameters](https://github.com/panthernet/ThunderED/wiki/Configure-settings.json)
  - Go one folder up `cd ..`
  - Build from source code: `docker build -t thundered .`
  - Your docker container name will be: `thundered:latest`
- 2B. Pull latest pre-compiled version. You can also specify release version to grab exact release `docker pull panthernet/thundered:1.4.1`
  - Run `docker pull panthernet/thundered`
  - Your docker container name will be: `panthernet/thundered:latest`

3. Prepare static data directory, for example: **mkdir /opt/thunder** and copy **settings.json** into newly created folder. Static directory will be used to store sensitive data which might need to persist between updates or easily accessed by bot admin. This data includes: **settings.json**, **edb.db**, **\_simplifiedAuth.txt**, **shipdata.json**, **Templates/Messages/\*.\*** and **Logs** directory. Database file named `edb.db` will be created in this folder automatically if you use SQLite database (default). You can also move `Languages` folder into static directory in case you want to edit them manually. Just make sure you set `"LanguageFilesFolder": "Data\Languages"` in config file. The bot will use **only** mentioned files from static data folder. All other files will be used from bot Docker container location.
4. Run bot in the mode you like:

- In the background: `docker run -d -p 8000:8000 -v /opt/thunder:/app/ThunderED/Data CONTAINER_NAME`
- Debug: `docker run -p 8000:8000 -v /opt/thunder:/app/ThunderED/Data CONTAINER_NAME`
- CONTAINER_NAME - name of the container from either 2A. or 2B. section

**WARNING: If you use Digital Ocean hosting please use search on #general channel on our Discord to solve possible IP/Port issues. In short: with DO you should add firewall rule to accept port 8000 as all ports there are closed by default.**

**Note**: Logs directory will also be located in static data directory (e.g. /opt/thunder)
