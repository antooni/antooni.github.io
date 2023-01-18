---
title: "Remap menu button in MacOS"
date: 2023-01-18
tags: ["MacOS", "Windows Keyboard"]
draft: false
---

# TL;DR

Here is the issue on Apple Stack Exchange [link](https://apple.stackexchange.com/questions/173898/repurposing-menu-button-on-windows-keyboards-used-in-os-x)
```
hidutil property --set '{"UserKeyMapping":[
    {
        "HIDKeyboardModifierMappingSrc": 0x700000065,
        "HIDKeyboardModifierMappingDst": 0x7000000E6
    }
]}'
```

# Problem

Recently I have started using MacOS. And with all this comfort connected with it, there also came a problem. Writing polish signs on my Bluetooth Keyboard (Microsoft Sculpture).

As you can see on the picture below, right to the spacebar there is an `Alt` key, which i used to click when I wanted to type polish sings e.g. `ą, ę`. 

![](https://m.media-amazon.com/images/I/81ZTerlRJ7L.jpg)

`Right Alt` is used in MacOS as `command`, but what I wanted is `option`. And yes, there is an easy way: you can swap option with command in `System Setting` for any keyboard, but...

I wanted a full MacOS experience, and "unify" my muscle memory, because switching from macbook keyboard to bluetooth would become hell. Not to mention remapping the macbook's keyboard keys, that is not what I wanted.

> I decided to remap the `≣ Menu` button to `⌥ Right option`

# Solution

Net-enjoyer truly I am, so I asked google and got the [answer](https://apple.stackexchange.com/questions/173898/repurposing-menu-button-on-windows-keyboards-used-in-os-x).

At first I tried `karabiner-elements`, but it neither helped me (did not support menu button), nor did I liked it (privacy issue, 3rd party listening to my keyboard).

So I went for the second answer, more low level one, using CLI tool called `hidutil` introduced in MacOS 10.12.

Steps I needed to take:

1. Identify which keys to change [cheatsheet](https://developer.apple.com/library/archive/technotes/tn2450/_index.html)
    - source: `≣ Menu` - Application (0x65)
    - destination: `⌥ Right option` - Right Alt (0xE6)

2. Run `hidutil` to test that it works:
``` 
hidutil property --set '{"UserKeyMapping":[
    {
        "HIDKeyboardModifierMappingSrc": 0x700000065,
         "HIDKeyboardModifierMappingDst": 0x7000000E6
    }
]}' 
```

3. Use `launchd` agent to run this sript on system startup

    - create file `~/Library/LaunchAgents/remap.plist`
    - fill the file with the following code

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.local.KeyRemapping</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/bin/hidutil</string>
        <string>property</string>
        <string>--set</string>
        <string>{"UserKeyMapping":[
            {
                "HIDKeyboardModifierMappingSrc": 0x700000065,
                "HIDKeyboardModifierMappingDst": 0x7000000E6
            }
        ]}</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
</dict>
</plist>
```

> It works !!! Proof: ćąłóę
