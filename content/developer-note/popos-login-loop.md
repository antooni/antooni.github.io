---
title: "Pop!_OS login issues"
date: 2022-11-07
tags: ["Linux", "Login loop"]
draft: false
---

# I cannot login to my system, plz help!

### 1. Try logging in text mode
Switch to text mode (Ctrl+Alt+F5) and try to login, if you are able to do it then the problem is with your graphical login manager.

### 2. Remove configuration files
To determine whether configuration in your home directory is causing the issue, you can create a new user account for testing purposes:
```
sudo adduser test
sudo systemctl reboot
```
If you're able to log in with the test user, the issue is somewhere in your regular user's home folder. Log into the full-screen terminal with your regular user again, and move some of the common configuration files out of the way:
```
mv ~/.config ~/.config.old
mv ~/.local ~/.local.old
mv ~/.cache ~/.cache.old
mv ~/.bashrc ~/.bashrc.old
mv ~/.zshrc ~/.zshrc.old
# and possibly many more, depending on your setup

sudo reboot

```
After moving those files and rebooting, try logging in again. 

🎉 **SOLVED my problem** 🎉

**.bashrc** was causing the problems. I put `exec zsh` in the beginning of this file. I do not exactly know why it caused this bug but will definitely research this one :-)

### 3. Reinstall login manager
You can reinstall GNOME Display Manager (which handles the login screen), along with the desktop environment. On Pop!_OS:

```
sudo apt install --reinstall gdm3 pop-desktop gnome-shell
sudo systemctl reboot
```

### 4. Reinstall drivers
The Nvidia or Radeon drivers can cause the bug, see this [tutorial](https://support.system76.com/articles/login-loop-pop/)


# References
Kudos to System76 team for once again solving my problem (previously I had one with bootloader).

- [System76 support article](https://support.system76.com/articles/login-loop-pop/)

- [Ubuntu gets stuck in login loop](https://askubuntu.com/questions/223501/ubuntu-gets-stuck-in-a-login-loop)
- [How to change graphic driver](https://askubuntu.com/questions/335285/how-to-change-proprietary-video-driver-using-the-command-line)