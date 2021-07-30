---
layout: single
title: "Setup Python development environment on Mac M1"
date: 2021-07-27
last_modified_at: 2021-07-27
tags:
  - macOS
  - Python
lang: en
---

## Problems

eventsourcing==8.2.5

pycryptodome==3.9.9:

```
../../Library/Caches/pypoetry/virtualenvs/sms-gb_s_ZWl-py3.8/lib/python3.8/site-packages/Crypto/Util/_raw_api.py:308: in load_pycryptodome_raw_lib
    raise OSError("Cannot load native module '%s': %s" % (name, ", ".join(attempts)))
E   OSError: Cannot load native module 'Crypto.Cipher._raw_ecb': Trying '_raw_ecb.cpython-38-darwin.so': dlopen(/Users/quanengineering/Library/Caches/pypoetry/virtualenvs/sms-gb_s_ZWl-py3.8/lib/python3.8/site-packages/Crypto/Util/../Cipher/_raw_ecb.cpython-38-darwin.so, 6): no suitable image found.  Did find:
E   	/Users/quanengineering/Library/Caches/pypoetry/virtualenvs/sms-gb_s_ZWl-py3.8/lib/python3.8/site-packages/Crypto/Util/../Cipher/_raw_ecb.cpython-38-darwin.so: mach-o, but wrong architecture
E   	/Users/quanengineering/Library/Caches/pypoetry/virtualenvs/sms-gb_s_ZWl-py3.8/lib/python3.8/site-packages/Crypto/Cipher/_raw_ecb.cpython-38-darwin.so: mach-o, but wrong architecture, Trying '_raw_ecb.abi3.so': dlopen(/Users/quanengineering/Library/Caches/pypoetry/virtualenvs/sms-gb_s_ZWl-py3.8/lib/python3.8/site-packages/Crypto/Util/../Cipher/_raw_ecb.abi3.so, 6): image not found, Trying '_raw_ecb.so': dlopen(/Users/quanengineering/Library/Caches/pypoetry/virtualenvs/sms-gb_s_ZWl-py3.8/lib/python3.8/site-packages/Crypto/Util/../Cipher/_raw_ecb.so, 6): image not found
```

pandas==1.2.4

```
  Original error was: dlopen(/private/var/folders/xb/3h3th3hn3djfqy95b4pnqd9h0000gp/T/pip-build-env-_s03ja09/overlay/lib/python3.8/site-packages/numpy/core/_multiarray_umath.cpython-38-darwin.so, 2): no suitable image found.  Did find:
  	/private/var/folders/xb/3h3th3hn3djfqy95b4pnqd9h0000gp/T/pip-build-env-_s03ja09/overlay/lib/python3.8/site-packages/numpy/core/_multiarray_umath.cpython-38-darwin.so: mach-o, but wrong architecture
  	/private/var/folders/xb/3h3th3hn3djfqy95b4pnqd9h0000gp/T/pip-build-env-_s03ja09/overlay/lib/python3.8/site-packages/numpy/core/_multiarray_umath.cpython-38-darwin.so: mach-o, but wrong architecture
```

```
brew install gdal
Updating Homebrew...
==> Auto-updated Homebrew!
Updated 1 tap (homebrew/core).
==> Updated Formulae
Updated 48 formulae.

Error: Cannot install in Homebrew on ARM processor in Intel default prefix (/usr/local)!
Please create a new installation in /opt/homebrew using one of the
"Alternative Installs" from:
  https://docs.brew.sh/Installation
You can migrate your previously installed formula list with:
  brew bundle dump
```

## Solution

Install x86 brew as main `brew` because:
* pass CFLAGS path is not enough
* pyenv install python got trouble


Install both x86 and arm64 Python executables => bullshit

Check which architecture Python executable is running on:

```
$ pipenv shell
$ file $(which python)
/Users/quanengineering/.local/share/virtualenvs/qcbe-Wd2sNm2o/bin/python: Mach-O 64-bit executable arm64
```

*Install the Xcode command line tools:*

```
sudo xcode-select --install
```

*Install Homebrew natively on Mac M1:*

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

*Install a copy of Homebrew running under under Rosetta 2 (x86_64 architecture):* (it can coexist with Homebrew Mac M1 version)

1. run the installation under Rosetta 2
```
arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. add alias to `.zshrc`:
```
alias brew86="arch -x86_64 /usr/local/bin/brew"
```

*Install pyenv:*

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

*Install build dependencies of pyenv:*

```
$ brew install openssl readline sqlite3 xz zlib
$ brew86 install openssl readline sqlite3 xz zlib
```

*Install x86 Python:*

1. run pyenv under x86 architecture by adding alias to `.zshrc`:
```
alias pyenv86="arch -x86_64 pyenv"
```

2. install [pyenv-alias](https://github.com/s1341/pyenv-alias) plugin to set alias for x86 Python version:

3. install Python 3.8.11 x86

```
VERSION_ALIAS="3.8.11_x86" pyenv86 install 3.8.11
```

4. Specify the version alias name using the `VERSION_ALIAS` environment variable when performing a `pyenv install`:

Comment to disable this line `eval "$(/opt/homebrew/bin/brew shellenv)"` in `.zshrc`:

```
CFLAGS="-I$(brew86 --prefix openssl)/include -I$(brew86 --prefix readline)/include" \
LDFLAGS="-L$(brew86 --prefix openssl)/lib -L$(brew86 --prefix readline)/lib" \

CFLAGS="-I$(brew86 --prefix readline)/include -I$(brew86 --prefix openssl)/include -I$(xcrun --show-sdk-path)/usr/include" \
LDFLAGS="-L$(brew86 --prefix readline)/lib -L$(brew86 --prefix openssl)/lib" \
VERSION_ALIAS="3.8.11_x86" \
pyenv86 install -v 3.8.11



CFLAGS="-I$(brew86 --prefix openssl)/include -I$(xcrun --show-sdk-path)/usr/include" \
LDFLAGS="-L$(brew86 --prefix openssl)/lib" \
VERSION_ALIAS="3.8.11_x86" \
pyenv86 install -v 3.8.11

```



 -I$(brew86 --prefix zlib)/include
 -L$(brew86 --prefix zlib)/lib

 -I$(xcrun --show-sdk-path)/usr/include

-L$(brew --prefix bzip2)/lib
-I$(brew --prefix bzip2)/include

PKG_CONFIG_PATH="$(brew86 --prefix openssl)/lib/pkgconfig" \

CFLAGS="-I$(brew --prefix bzip2)/include"
LDFLAGS="-L$(brew --prefix zlib)/lib -L$(brew --prefix bzip2)/lib"



## References

[http://sixty-north.com/blog/pyenv-apple-silicon.html](http://sixty-north.com/blog/pyenv-apple-silicon.html)


Note: for Mac M1: to avoid get stuck when import database => use this image https://hub.docker.com/r/gangstead/postgis to create postgres instance
