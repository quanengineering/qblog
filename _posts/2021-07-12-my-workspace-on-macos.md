---
layout: single
title: "My Workspace on macOS"
date: 2021-07-12
last_modified_at: 2021-07-13
tags:
  - Linux
  - macOS
lang: en
---

Here are things I do after installing macOS Big Sur on Mac M1.

## Install Miscellaneous Tools
* [Chrome](https://www.google.com/chrome/) (choose Apple Chip version)
* [KeePassXC](https://keepassxc.org/download/#mac) (choose Apple Chip version)
* [Dropbox](https://www.dropbox.com/install)
* [EVKey](https://evkeyvn.com/) (Vietnamese Input)

## Install Communication Tools
* [Skype](https://www.skype.com/en/get-skype/)
* [Slack](https://slack.com/intl/en-vn/downloads/mac)
* [Microsoft Outlook](https://www.office.com/)

## Install Developer Tools
* [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh/wiki) (you don't need to zsh because macOS Big Sur comes with zsh as the default shell)
* [iTerm2](https://iterm2.com/downloads.html) (as an alternative to Terminator on Ubuntu)
* [Docker](https://docs.docker.com/docker-for-mac/install/) (choose Apple Chip version)
* [Jetbrains IDEs](https://www.jetbrains.com/help/idea/installation-guide.html#toolbox) (choose Apple Chip version)
* [VS Code](https://code.visualstudio.com/)
* [Postman](https://www.postman.com/downloads/)

### Node Version Manager

Steps to install Node Version Manager on Mac M1:
1. manually install the Xcode command line tools before running the NVM install
```
sudo xcode-select --install
```
2. Optional: create zshrc if it is not exists
```
touch ~/.zshrc
```
3. install nvm automatically - check [https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm) for the latest version
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
4. install Nodejs v15+ (works on arch64 for Mac M1)
```
nvm install v15
```

### Homebrew

*Install Homebrew natively on Mac M1*:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

*Install a copy of Homebrew running under under Rosetta 2 (x86_64 architecture)* (it can coexist with Homebrew Mac M1 version):
1. run the installation under Rosetta 2
```
arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
2. run this line before running any command to force Brew run with x86_64 architecture:
```
eval $(/usr/local/bin/brew shellenv)
```

### Pyenv

Steps to install pyenv on Mac M1:
1. Run the automatic installer:
```
curl https://pyenv.run | bash
```

2. Add these lines to `.zshrc`:
```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"
```

### Pipenv

You can use pip3 of the Xcode command line tools to install pipenv:

```
pip3 install --user pipenv
```

Then add this line to `.zshrc`:

```
export PATH="/Users/your-username/Library/Python/3.8/bin:$PATH"
```

To upgrade pipenv at any time:

```
pip3 install --user --upgrade pipenv
```

### Python

As the time of writing, pyenv can install Python 3.7.11, 3.8.11, 3.9.6 on Mac M1 natively without any interruption, but it's not the case for Python 3.6.14 because it will get stuck at the building process.

The solution to install Python 3.6.14 is to run the installation under Rosetta 2. Here are steps to install:
1. install a copy of Homebrew running under Rosetta 2.
2. run a copy of Terminal under Rosetta 2:
    * Locate the Terminal application within the Applications folder.
    * Right-click on it and choose "Duplicate".
    * Rename the duplicated Terminal app to something like "Rosetta Terminal".
    * Right-click the "Rosetta Terminal" app and choose "Get Info".
    * Check "Open using Rosetta", then close the Get Info window.
    * Now you can open the "Rosetta Terminal" app to run Terminal under Rosetta 2.
3. force Brew run with x86_64 architecture:
```
eval $(/usr/local/bin/brew shellenv)
```
4. install the Python build dependencies:
```
brew install openssl readline sqlite3 xz zlib
```
5. install Python with arm64 patch:
```
pyenv install --patch 3.6.14 < <(curl -sSL https://github.com/python/cpython/commit/8ea6353.patch\?full_index\=1)
```