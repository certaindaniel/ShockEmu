[![macos-bigsur](https://img.shields.io/badge/macos-bigsur-brightgreen.svg)](https://www.apple.com/macos/big-sur/)

# Key Mapping
`only_keyboard.se` goes like this:

![Key Mapping](https://github.com/backslash-f/ShockEmu/blob/master/KeyMapping.png)

# Requirements

- It depends on your system having [PS Remote Play](https://remoteplay.dl.playstation.net/remoteplay/lang/en/index.html) installed at `/Applications/RemotePlay.app`. If this is not the case, you'll need to modify `run.sh` accordingly.

- The `OS X Command Line Tools` [needs to be installed](https://stackoverflow.com/a/53078282/584548).

- Relies on `Python 3`, which can be installed via `brew install python`

- You have to [turn off System Integrity Protection via 'csrutil'](https://www.imore.com/how-turn-system-integrity-protection-macos) in order for `DYLD_INSERT_LIBRARIES` to function on the newest macOS. (Thanks [Ben](https://github.com/benh57) for figuring this out!)

# Setup
```zsh
./build.sh only_keyboard.se
./run.sh
```

# SE File Format
SE files are, generally speaking, a mapping between an input key, mouse button, or mouse movement to a DualShock input. See the example file (`example.se`) for a breakdown of the format.

# How It Works
ShockEmu works by intercepting the IOHID calls of PS Remote Play application and presents an emulated DualShock controller. It also hooks into the input routines of the application, to catch keyboard and mouse inputs, which then get mapped according to your SE file.

# Pro Tip
The `alias` below allows for typing `play` / `enter` anywhere in `Terminal` and have `RemotePlay.app` launched with the above keys mapped:
```
$ cat ~/.zshrc | grep play
alias play="pushd [REPOSITORY_ROOT]; ./run.sh &; popd"
```
👆🏻`ShockEmu` repo location must be updated according to your machine.
