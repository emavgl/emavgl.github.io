+++
authors = ["Emanuele Viglianisi"]
title = "How to connect Apple Magic Keyboard with multiple devices"
date = "2023-09-27"
description = "Connect the Apple Magic Keyboard with multiple device using Bluetooth"
tags = [
    "apple",
    "keyboards",
    "bluetooth",
    "scripts",
    "macos",
    "windows",
    "linux",
]
categories = [
    "automation",
    "customization"
]
+++

# How to connect Apple Magic Keyboard with multiple devices

Apple Magic Keyboard is one of the most famous / fun-to-use keyboards. I recently got one and wanted to use it with multiple computers and OS. In particular, I mainly use the keyboard connected via Bluetooth to my MacBook Pro, and I'd like to use it with a computer that has both Windows and Ubuntu operative systems.

The Apple Magic Keyboard, differently than other competitors’ keyboards like Logitech MX Keys, does not support multiple devices. It can be paired just with one device at a time.

Every time I’d like to switch from Mac OS to Windows, for example, I need to:

- Open Bluetooth control panel
- Forget the device
- Search and pair again the device

It is quite a tedious procedure, therefore I have tried to automate it as much as possible and this is what I have obtained.

## Sharing the Bluetooth pairing key

Following the procedure in this [article](https://nelsonaloysio.medium.com/how-to-share-bluetooth-pairing-key-among-linux-macos-windows-2714ef40daff), I have tried to share the same pairing key between Mac OS and Windows. However, it did not work for me - the device connects, but after a few seconds, it disconnects automatically.

I believe, the Keyboard registers the MAC address of the connected device and sticks with that until it is unpaired and paired again. Sharing the pairing key would work fine instead when you want to use the Keyboard with two OS in dual-boot.

## Sharing the Bluetooth MAC address

If the MAC address is the problem, can the two devices share the same Bluetooth MAC address, so that the keyboard recognizes them as the same device? Yes, it could be an option. Some Bluetooth devices allow you to change the MAC address. However, the MAC address is designed to be unique, and it is not a good idea to have two devices with the same MAC address, also, not all the Bluetooth hardware supports changing MAC address. If you really want to try that, you can check out this [program for Windows](https://macaddresschanger.com/).

## Methods for a fast pairing process

After giving up finding a way for my keyboard to be recognized by all my devices and operative system without repeating the pairing process, I have focused on making that process easier, quick, and with the minimum number of clicks.

### **Mac OS**

I found that the fastest way to pair the Magic Keyboard to the Mac Book is just plugging it by using a simple Lightning cable. After connecting it, it is automatically paired and you can use it simply with Bluetooth.

Windows and Linux don’t have this functionality Bluetooth-pairing-by-plugging-a-cable functionality and I had to find another way.

If you prefer having a script like for Linux and Windows, you may want to use the command line tool [https://github.com/toy/blueutil](https://github.com/toy/blueutil).

### **Linux**

- Make sure you have installed the *bluez* package

```bash
sudo apt update
sudo apt install bluez
```

- Find the Keyboard MAC address

Turn off and turn on your Keyboard to turn the discovery mode. Then run the command

```bash
bluetoothctl scan on
```

and note the MAC address (looks like 01:23:45:AB:CD:9F).

- Create a bash script:

```bash
#!/bin/bash

keyboard_mac="<YOUR_KEYBOARD_MAC_ADDRESS>"
bluetoothctl remove $keyboard_mac
sleep 2
bluetoothctl agent on
bluetoothctl default-agent

stdbuf -oL bluetoothctl scan on | while IFS= read -r line; do
    echo $line

    # Check if the target string is present in the line using grep
    if [[ $line == *"$keyboard_mac"* ]]; then
        echo "Found '$keyboard_mac' in the output. Stopping the program..."
        # Terminate the program gracefully
        pkill -P $$  # Terminate all child processes (including 'your_program')
        break
    fi
done

bluetoothctl trust $keyboard_mac
bluetoothctl pair $keyboard_mac
bluetoothctl connect $keyboard_mac
```

The script will remove the keyboard if already paired. Then will search again for the device and pair for it. During the `bluetoothctl pair` command the system will show you a prompt like “Do you want to connect this device with the PIN…” at this point, click Connect and the device will be immediately ready to be used.

***Important:** you have to make the keyboard enter in the discovery mode. To do that, just turn it off and turn it on again.*

I then created a Desktop shortcut with this configuration

```bash
$ cat magickeyboard.desktop 
[Desktop Entry]
Categories=Application;
Exec=bash /home/emavgl/magickeyboard.bash
Icon=utilities-terminal
Name=Pair Magic Keyboard
```

Pairing the Keyboard is just as easy as:

- Turning off and On the Keyboard
- Double Click on the program
- Click `Accept` when prompted to pair the device

### Windows

A similar procedure is also possible on Windows.

- First, it is necessary to install [Bluetooth command line tools - work with bluetooth from the command line (bluetoothinstaller.com)](https://bluetoothinstaller.com/bluetooth-command-line-tools) - when installing, ensure to enable the options to add the command to the PATH.
- Find the Keyboard MAC address by opening the `cmd` and running the command `btdiscovery`. In a couple of seconds, you will see on the screen the list of the devices with their MAC address.

***Important:** you have to make the keyboard enter in the discovery mode. To do that, just turn it off and turn it on again.*

- Create a bat file

```java
@ECHO OFF
:: Store the MAC address in a variable
set "mac_address=<KEYBOARD-MAC-ADDRESS-HERE>"
echo "Remove association between COM port and a remote service"
btcom -b"%mac_address%" -r -s1124
echo "Unpair the device"
btpair -u -b"%mac_address%"
echo "Create association between COM port and a remote service"
btcom -b"%mac_address%" -c -s1124
```

Note that `1124` is the Bluetooth service code for the Keyboard (HumanInterfaceDeviceService). If you want to pair the headphones, you have to add voice service `111e`,  and music `110b`. You can find [here](https://www.bluetooth.com/specifications/assigned-numbers/) the list of services.

Pairing the Keyboard is just as easy as:

- Turning off and On the Keyboard
- Double Click on the .bat script
- Click `Accept` when prompted to pair the device


Finally, I can enjoy my Keyboard in all my devices. I hope this guide was also useful to you!