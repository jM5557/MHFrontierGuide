---
title: "Troubleshooting"
slug: "troubleshooting"
backgroundImage: "assets/images/bg-collage.jpg"
foo: "bar"
---
# Troubleshooting

While this guide tries to provide instructions as simple as possible, it does not account for possible problems that may occurr.

Below are several issues that have been observed, alongside some cataloged potential fixes:

## run_client.bat does not open, quickly flashes, or displays an error

If you see this Python Error:

```
frida.NotSupportedError: unable to spawn executable at 'mhf.exe': 0x000002e4
```

Then you haven't ran the file run_client.bat as administrator. In order for the client to start, you must run this file as administrator EVERY TIME you want to play the game. You can do this by right-clicking and selecting **Run as Administrator**

**Tip:** If you do NOT want to go through this step every time you wish to play the game, you can **right-click > Create Shortchut** Next, make this shortcut always run as administrator via **right-click > Properties > Advanced > Run as Administrator**

![create shortcut](assets/images/troubleshooting-create-client-shortcut-0.jpg)

![run shortcut as admin](assets/images/troubleshooting-create-client-shortcut-1.jpg)

## Game does not start after running the client

If you run the client and then see a window mail-carrier Felyne and Japanese text on the right-side, then you forgot to run the server! The server is not running, which means the client is unable to authenticate and connect.

If you completed the initial setup successfully, then double-click the file run_server.bat and run_client.bat afterwards.

![felyne that has fallen and can't get up](assets/images/troubleshooting-servers-down.jpg)
