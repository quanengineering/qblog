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

2. Add pyenv executable to PATH by adding the following to `~/.profile` and `~/.zprofile`:
```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
```

3. Load pyenv into the shell by adding the following to `~/.zshrc`:
```
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

Make sure to restart your entire logon session for changes to profile files to take effect.

### pipx

1. Use pyenv to install the latest version of Python, then use it to install pipx
```
pyenv install 3.9.6
pyenv global 3.9.6
pip install --user pipx
```

2. declare installation directory in `.zshrc`:
```
export PATH="/Users/your-username/.local/bin:$PATH"
```

To upgrade pipx at any time:

```
pip install --user -U pipx
```

### Pipenv

Use pipx to install:

```
pipx install pipenv
```

### Poetry

Use pyenv to switch between Python versions and use pip to install:

```
pip install poetry
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

## Tips

### Install `psycopg2-binary`

Follow [this workaround](https://github.com/psycopg/psycopg2/issues/1200#issuecomment-776159466):

```
brew install postgresql

LDFLAGS="-L/opt/homebrew/opt/openssl@1.1/lib" CPPFLAGS="-I/opt/homebrew/opt/openssl@1.1/include" PKG_CONFIG_PATH="/opt/homebrew/opt/openssl@1.1/lib/pkgconfig" pip install psycopg2-binary
```

### Install `grpcio`

If you get errors, please refer some workarounds in [this guide](https://github.com/grpc/grpc/issues/24677), for example:

```
GRPC_PYTHON_BUILD_SYSTEM_ZLIB=true pip install grpcio
```

### Install `pyicu`

1. run a copy of Terminal under Rosetta 2, then force Brew run with x86_64 architecture:
```
eval $(/usr/local/bin/brew shellenv)
```

2. install libicu:
```
brew install pkg-config icu4c
```

3. temporarily prepend PATH according to the information provided by `brew info icu4c`:
```
PATH="/usr/local/opt/icu4c/bin:/usr/local/opt/icu4c/sbin:$PATH"
```

4. install `pyicu`:
```
pip3 install pyicu
```
