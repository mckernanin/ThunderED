---
id: webserver-setup
title: Web Server Setup
---

**Updated for V1.4.1**

### DESCRIPTION

Web server is a built-in module that provides an access to a series of web pages required to authenticate or setup differen modules. You will need it for the following modules: `ModuleAuthWeb, ModuleNotificationFeed, ModuleTimers, ModuleMail, ModuleHRM, ModuleContractNotifications, ModuleWebConfigEditor, ModuleIndustrialJobs, etc.`

### SETUP

1. Open config file `settings.json`
2. Enable following modules: `"ModuleWebServer": true`
3. Find config section `WebServerModule` and set `WebExternalIP`/`WebExternalPort` properties. This will be your IP/Domain address and port to access ThunderED web server.
4. Set `CcpAppClientId` and `CcpAppSecret` from the CCP application you created during setup process.
5. Configure your OS /Docker/Router so the specified address is accessible from the internet. If everything is set correctly then you will see initial web page by following the IP:PORT address.
