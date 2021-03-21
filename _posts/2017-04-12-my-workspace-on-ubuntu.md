---
layout: single
title: "My Workspace on Ubuntu"
date: 2017-04-12
last_modified_at: 2021-03-11
tags:
  - Linux
lang: en
---

Here are things I do after installing Ubuntu 20.04.

## Fix time conflict

The installation of Ubuntu alongside an existing Windows 10 causes a time conflict when switching between these two operating systems. It is because Ubuntu sets the hardware clock (CMOS clock, the BIOS time) to UTC while Windows is local time.

I always use this command to force the Ubuntu to use the local time.

```
$ timedatectl set-local-rtc 1 --adjust-system-clock
```

## Tweak the Dock panel

It is more convenient for me when the Dock is displayed at the bottom center of the screen.

To begin with, I can easily set the Dock to the bottom by using the default System Settings dialog.

The next step is to set the Dock to the center. To do that, I have to use this command to set the turn off the extend-height setting.

```
$ gsettings set org.gnome.shell.extensions.dash-to-dock extend-height false
```

## Install Web Browsers
* [Chrome](https://www.google.com/chrome/)
* [Microsoft Edge](https://www.microsoftedgeinsider.com/en-us/download)
* [Firefox](https://www.mozilla.org/en-US/firefox/new/)

## Install Communication Tools
* [Skype](https://www.skype.com/en/get-skype/)
* [Telegram](https://www.omgubuntu.co.uk/2019/08/how-to-install-telegram-on-ubuntu)
* [Slack](https://slack.com/downloads/linux)
* [Discord](https://discord.com/download)
* [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app)

## Install Developer Tools
* [Git](https://git-scm.com/download/linux)
* [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh/wiki)
* [Terminator](https://github.com/gnome-terminator/terminator/blob/master/INSTALL.md)
* [Docker](https://docs.docker.com/engine/install/ubuntu/)
* [Postman](https://speedysense.com/install-postman-on-ubuntu-20-04/)
* [htop](https://htop.dev/downloads.html)
* [mkcert](https://github.com/FiloSottile/mkcert)
* [Jetbrains IDEs](https://www.jetbrains.com/help/idea/installation-guide.html#toolbox)
* [VS Code](https://code.visualstudio.com/)

## Install Miscellaneous Tools
* [KeePass](https://sourceforge.net/p/keepass/discussion/329220/thread/17d1bd26/)
* [Dropbox](https://www.dropbox.com/install)
* [Flameshot](https://github.com/flameshot-org/flameshot/releases)
* [Vietnamese Input](https://github.com/BambooEngine/ibus-bamboo)
* [NetSpeed](https://ubuntuhandbook.org/index.php/2020/06/download-upload-speed-ubuntu-20-04-panel/)
