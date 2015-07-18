---
layout: post
title: Yubikey & KeePass cross platform
type: post
status: publish
published: true
---

A while back i got a [Yubikey Neo and a Neo-n](https://www.yubico.com/products/yubikey-hardware/yubikey-neo/) they are cool little devices that can work as the second part of a 2 factor authentication. The **Neo** apart from usb also supports Nfc so it can be used with most modern Android phones. So here's a short summary of how to get it all working. To get everything to work you need to install the [KeeChallenge](http://sourceforge.net/projects/keechallenge/) plugin in KeePass, I used the latest version (2.29) when setting everything up. The trick is to put the password file on something shared that everything can read usb stick, Dropbox or similar.

### KeePass on windows
For windows follow [this](http://www.kahusecurity.com/2014/securing-keepass-with-a-second-factor/) guide. Don't forget to copy the files from the [YubiKey-Personalization release](https://developers.yubico.com/yubikey-personalization/Releases/).

### KeePass on OSX
On OSX the use following [guide](http://forum.yubico.com/viewtopic.php?f=8&t=1337#p6091). A bit more hands on work but just follow the steps. Currently it seems like mono 4.0.2 doesn't work so go with 4.0.1.

### KeePass on Android
On android you need the [Keepass2Android Password Safe](https://play.google.com/store/apps/details?id=keepass2android.keepass2android) and [YubiChallenge](https://play.google.com/store/apps/details?id=com.yubichallenge) and a phone that supports Nfc, most modern Android phones do.

### iOS
Nope, return in a couple of years when iOS has working nfc support