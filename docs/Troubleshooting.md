---
id: troubleshooting
title: Troubleshooting
---

**ADVICE**: [Join our Discord group](https://discord.gg/UsnY6UR) and check pinned messages in #general channel. You can also ask your questions there and we will answer them if possible.

## Issues report guidelines

- If there's an error in the console log, search for the detailed error message in the log file and post it with your report. The name of the log file can be identified by the text in the square brackets on the console message. Example: `12:49:34 [ Module] [ Notification]: Inititalizing Notifications module...` where `Notification` is the name of the log file. `Logs` folder is located in the app directory but if you use Docker under Linux then it will be located in the bound `Data` folder instead.
- If there's a problem related to EVE Notifications feed then find original notification message in `notifications_lg.log` log file and attach it to your report.
- If your problem is related to the module configuration, make sure you attach corresponding config section from `settings.json` file to your report. You can omit sensitive data such as IDs but the general config layout will be helpful.

### Console log spams "Starting Web Server" message

This behavior means that bot app can't initialize built-in web server using the settings specified in **settings.json** file. Usually it means that specified port is being used by another application or is closed by your OS/router/provider/whatever. If your host machine don't have direct access to your internet IP (e.g. you use router hardware) may be it is wise to configure port forwarding to route requests from you external IP:PORT to internal network IP:PORt available to your host machine.

WARNING: If you use Digital Ocean hosting please use search on #general channel on our Discord to solve possible IP/Port issues. In short: with DO you should add firewall rule to accept port 8000 as all ports there are closed by default.

### CPU load is very high when bot is running in a background (service)

Set `"RunAsServiceCompatibility": true` in config file. This will disable all implemented console interactions and should lessen the CPU load.

### Console log displays some error messages colored in RED

Contact me on Discord or create new issue on GitHub and we will get it sorted out and fixed!

### MySQL database connection throws an error like **EnsureDBExists**

Docker runs inside its own container so to access MySQL you will have to allow remote connections to the database and then connect to it via public ip instead of localhost. When you use localhost on Docker it tries to look for a MySQL inside the Docker container.
