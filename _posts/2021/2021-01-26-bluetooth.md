---
layout: post
title: Bluetooth
date: 2021-01-26
categories: linux
tags: [bluetooth, ubuntu]

---
This short article explains how to connect to a bluetooth device from the command line on Ubuntu 20.04.

<!--more-->

To establish which bluetooth devices are available, type the command `bluetoothctl devices`. The output should be similar to the following, providing the MAC address and name of the devices found;

```c
Device 00:A0:DE:06:5B:76 YBA-11 Yamaha
```

To connect to the device, use the following command (remembering of course to change the MAC address to that associated with your device).

```c
echo "connect 00:A0:DE:06:5B:76" | bluetoothctl
```

To automatically connect to the device at login, we first need to add the device to the list of trusted devices. This is done by running the following;

```c
bluetoothctl trust 00:A0:DE:06:5B:76
```

Next, create `connect-bluetooth.sh` and save it to ~/bin. Add the following to it;

```c
#!/bin/bash
bluetoothctl
sleep 15
echo "connect 00:A0:DE:06:5B:76" | bluetoothctl
exit
```
Make the script executable;

```c
chmod +x ~/bin/connect-bluetooth.sh
```

To run the script and connect to the bluetooth device automatically at login, and assuming you are using the i3 window manager, add the following to `~/.config/i3/config`;

```c
exec --no-startup-id ~/bin/connect-bluetooth.sh
```
