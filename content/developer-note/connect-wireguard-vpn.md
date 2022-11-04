---
title: "Connect to VPN using Wireguard"
date: 2022-11-05
tags: ["VPN", "Wireguard"]
draft: false
---

# Connect to VPN on startup

## Tutorial for Linux (Ubuntu)
 
1. Install Wireguard `sudo apt-get wireguard`
2. Download `.conf` VPN configuration file from your provider
3. Put this file inside `/etc/wireguard`
4. Create a script responsible for connection and save it to your local disk
    ```
    sudo wg-quick up <name>
    ```
    where name is a name of the file inside `/etc/wireguard` (without .conf extension)
5. To run this script on startup type in terminal: `sudo crontab -e`
6. At the bottom of the opened file add `@reboot <your/script/path>`

### References
- [Run file on startup as root](https://askubuntu.com/questions/290099/how-to-run-a-script-during-boot-as-root)