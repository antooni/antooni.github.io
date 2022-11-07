---
title: "Encrypted DNS"
date: 2022-11-05
tags: ["DNS", "Encryption"]
draft: false
---

# Encrypt DNS traffic

Recently, I have been setting up VPN connection and during network sniffing with [Wireshark](https://www.wireshark.org/) I found out that all my DNS request are plain text, so there is a room to potentially see all my DNS request. What it effectively means is that a third party can observe my internet connection and see which pages I visit. To be precise, just the addresses, not the content, so it is not that much of a vulnerability, but still...

So I googled **how to encrypt DNS traffic**, the first thing that popped up was [Cloudflare's 1.1.1.1](https://developers.cloudflare.com/1.1.1.1/encryption/). They introduced to me the concept of [DNS over TLS (DoT)](https://developers.cloudflare.com/1.1.1.1/encryption/dns-over-tls/) and [DNS over HTTPS](https://developers.cloudflare.com/1.1.1.1/encryption/dns-over-https/).

It turns out that you can easily encrypt you DNS traffic on Android phones and inside your Web Browser.

## Tutorials

### [Android](https://developers.cloudflare.com/1.1.1.1/setup/android/)

1. Go to Settings > Network & internet.
2. Select Advanced > Private DNS.
3. Select the Private DNS provider hostname option.
4. Enter one.one.one.one or 1dot1dot1dot1.cloudflare-dns.com and press Save.

### [Linux](https://developers.cloudflare.com/1.1.1.1/setup/linux/) (almost the same for other OS)

1. Go to Show Applications > Settings > Network.
2. Select the adapter you want to configure — like your Ethernet adapter or WiFi card — and select the Settings button.
3. On the IPv4 tab > DNS section, disable the Automatic toggle.

4. Set DNS resolvers to 
    ```
    1.1.1.1
    1.0.0.1
    ```

5. Go to IPv6.

6. Set DNS resolvers to
    ```
    2606:4700:4700::1111
    2606:4700:4700::1001
    ```
7. Select Apply.
### [Mozilla](https://developers.cloudflare.com/1.1.1.1/encryption/dns-over-https/encrypted-dns-browsers/)

1. Select the menu button > Settings.
2. In the General menu, scroll down to access Network Settings.
3. Select Settings.
4. Select Enable DNS over HTTPS. By default, it resolves to Cloudflare DNS.

## Verification

To find out whether you set it up correctly visit https://1.1.1.1/help. 

## Final remarks

Encrypting your DNS traffic is a pretty new concept, the standards have not been well established yet. I will definitely put more thought and do more research on it in the future. For now I will settle with trusting Cloudflare... Future will tell whether it was a good choice.


# ! CAUTION !
Setting your DNS server manually is a responsible task and I do not take responsibility for any potential misconfigurations. Do it at your own risk! 

