[![macos-bigsur](https://img.shields.io/badge/macos-bigsur-brightgreen.svg)](https://www.apple.com/macos/big-sur/)

# Key Mapping
`only_keyboard.se` goes like this:

![Key Mapping](https://github.com/backslash-f/ShockEmu/blob/master/Images/KeyMapping.png)

# Requirements

- It depends on your system having [PS Remote Play](https://remoteplay.dl.playstation.net/remoteplay/lang/en/index.html) installed at `/Applications/RemotePlay.app`. If this is not the case, you'll need to modify `run.sh` accordingly.

- The [latest `Command Line Tools`](https://developer.apple.com/download/more/) needs to be installed.

- Relies on `Python 3` (kudos to [willoftw](https://github.com/willoftw)). `brew install python`

- You have to [turn off System Integrity Protection via 'csrutil'](https://www.imore.com/how-turn-system-integrity-protection-macos) in order for `DYLD_INSERT_LIBRARIES` to function on the newest macOS. (Thanks [Ben](https://github.com/benh57) for figuring this out!)

# Setup
```zsh
./build.sh only_keyboard.se
./run.sh
```

# SE File Format
SE files are, generally speaking, a mapping between an input key to a DualShock input. See the `only_keyboard.se` file for a breakdown of the format.

# How It Works
ShockEmu works by intercepting the IOHID calls of PS Remote Play application and presents an emulated DualShock controller. It also hooks into the input routines of the application to catch keyboard inputs, which then get mapped according to your SE file.

# Pro Tips

### Launch from Terminal
The `alias` below allows for typing `play` / `enter` anywhere in `Terminal` and have `RemotePlay.app` launched with the above keys mapped:

```bash
$ cat ~/.zshrc | grep play
alias play="pushd [REPOSITORY_ROOT]; ./run.sh &; popd"
```

### Launch from Terminal + Key Mapping Image
Have `Preview` opening the key mapping image for you and `RemotePlay.app` launched:

![Key Mapping + Remote Play](https://github.com/backslash-f/ShockEmu/blob/master/Images/KeyMapping_PSRemotePlay.png)

Save this script somewhere (e.g.: `[SCRIPT_DIR]/play.sh`)

```bash
#!/bin/bash

SHOCK_EMU=$'[REPOSITORY_ROOT]'

open -a Preview $SHOCK_EMU/Images/KeyMapping.png

pushd $SHOCK_EMU
./run.sh &
popd
```

`chmod a+x` it and create an `alias` that looks like this:
```bash
$ cat ~/.zshrc | grep play
alias play=[SCRIPT_DIR]/play.sh
```

Enjoy! 🎮
