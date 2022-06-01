---
layout: post
title: Autostart NordVPN
date: 2021-01-27
categories: [linux, security]
tags: [server, vpn]
excerpt:
  This short article explains how we ensure NordVPN is activated at system startup, a solution of particular use when running a headless server.
---

How do we ensure NordVPN is activated at system startup? This short article explains how it's done. The solution is particularly helpful when running a headless server; once the process described below has been completed, the script will require no user input during subsequent reboots.

We begin by writing a very simple script, `nordvpn-connect.sh` and saving it to ~/bin.

```c
#!/bin/bash
#
# ~/bin/nordvpn-connect.sh
#
nordvpn connect United_Kingdom
exit 0
```

Next, create a file `nordvpn-connect.service` and save it to `/etc/systemd/system`. Add the following text to the new file, remembering to replace [user] with your own user name;

```c
[Unit]
After=network.service

[Service]
ExecStart=/home/[user]/bin/nordvpn-connect.sh

[Install]
WantedBy=default.target
```

Next, run the following commands in sequence;

```c
sudo chmod 755 /etc/systemd/system/nordvpn-connect.service
sudo chmod 755 /home/[user]/bin/nordvpn-connect.sh
sudo systemctl daemon-reload
sudo systemctl enable nordvpn-connect.service
```

Having enabled the service, the script associated with `nordvpn-connect.service` will be run every time the computer boots. NordVPN will automatically connect with no need for any input from the user.

Reboot the computer and type `nordvpn status` at the command line. All being well this should confirm NordVPN is connected.
