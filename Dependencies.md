# Summary
Below is a complete list of dependencies required for all servers. Use your distros package manager (apt-get, yum etc) to install these requirements.

> These dependencies should be installed before installing any LGSM server.

### Engine/Game
* [Source Engine](#Source-Engine)
* [Gold Source Engine](#Gold-Source-Engine)

# Notes
## Distro Compatibility
The older the server the less likely the game server will work on your server. For example _CentOS 5_ does not work with most servers. However _CentOS 6_ can but may require _glibc_ fixes.

### Recommended Distros
The below servers are the most compatible and work well with all servers.

* ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) => Ubuntu 12.04 LTS
* ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS 7

### Other Distros
Any distro with _=> GLIBC 2.15_ and _=> tmux 1.6_ will also be compatible with all servers.

### Glibc Compatibility

Different Servers have a different Glibc requirements. For example _Counter Strike: Source_ requires _2.07_, whereas _Garry's Mod_ requires _2.15_.

To check this take a look at the [[Glibc]] Wiki page

## CentOS 6 EPEL
LGSM requires you install [EPEL](http://download.fedoraproject.org/pub/epel/6/i386/repoview/epel-release.html) if running CentOS 6.

This is because tmux is not available as a standard package in CentOS 6.
## Ubuntu Releases
Only LTS releases are listed here as the dependencies don't normally change between LTS releases. However if a difference is found a non LTS release will be added until the newer LTS release is available.

# <a name="Source-Engine"></a>Source Engine
Counter Strike: Global Offensive, Counter Strike: Source, Half Life 2:Deathmatch etc.

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS
| Distro        | Arch | Dependencies                                                       |
| ------------- | ---- | :----------------------------------------------------------------- |
| CentOS 6      | x32  | tmux gdb mailx postfix libgcc_s.so.1 glibc                         |
| CentOS 6      | x32  | tmux gdb mailx postfix libgcc_s.so.1 glibc.i686 ncurses-libs.i686  |
| CentOS 7      | x64  | tmux gdb mailx postfix glibc.i686 libstdc++.i686 ncurses-libs.i686 |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian
| Distro        | Arch | Dependencies                                                     |
| ------------- | ---- |:---------------------------------------------------------------- |
| Debian 6      | x32  | tmux gdb mailutils postfix ca-certificates                       |
| Debian 6      | x64  | tmux gdb mailutils postfix ca-certificates lib32gcc1 lib32tinfo5 |
| Debian 7      | x32  | tmux gdb mailutils postfix ca-certificates                       |
| Debian 7      | x64  | tmux gdb mailutils postfix ca-certificates lib32gcc1 lib32tinfo5 |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu
| Distro           | Arch | Dependencies                                                     |
| ---------------- | ---- |:---------------------------------------------------------------- |
| Ubuntu 12.04 LTS | x32  | tmux gdb mailutils postfix libstdc++6:i386                       |
| Ubuntu 12.04 LTS | x64  | tmux gdb mailutils postfix lib32gcc1 libstdc++6:i386 lib32tinfo5 |
| Ubuntu 14.04 LTS | x32  | tmux gdb mailutils postfix libstdc++6:i386                       |
| Ubuntu 14.04 LTS | x64  | tmux gdb mailutils postfix lib32gcc1 libstdc++6:i386 lib32tinfo5 |

## Other
| Distro           | Arch | Dependencies                   |
| ---------------- | ---- |:------------------------------ |
| Gentoo           | x32  | gdb mailutils postfix iproute2 |

# <a name="Gold-Source-Engine"></a>Gold Source Engine
Counter Strike 1.6, Deathmatch Classic etc.
## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS
| Distro        | Arch | Dependencies                      |
| ------------- | ---- | :-------------------------------- |
| CentOS 6      | x32  | tmux gdb mailx postfix glibc      |
| CentOS 6      | x32  | tmux gdb mailx postfix glibc.i686 |
| CentOS 7      | x64  | tmux gdb mailx postfix glibc.i686 |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian
| Distro        | Arch | Dependencies                                         |
| ------------- | ---- |:---------------------------------------------------- |
| Debian 6      | x32  | tmux gdb mailutils postfix ca-certificates           |
| Debian 6      | x64  | tmux gdb mailutils postfix ca-certificates lib32gcc1 |
| Debian 7      | x32  | tmux gdb mailutils postfix ca-certificates           |
| Debian 7      | x64  | tmux gdb mailutils postfix ca-certificates lib32gcc1 |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu
| Distro           | Arch | Dependencies                                                     |
| ---------------- | ---- |:---------------------------------------------------------------- |
| Ubuntu 12.04 LTS | x32  | tmux gdb mailutils postfix                                       |
| Ubuntu 12.04 LTS | x64  | tmux gdb mailutils postfix lib32gcc1                             |
| Ubuntu 14.04 LTS | x32  | tmux gdb mailutils postfix                                       |
| Ubuntu 14.04 LTS | x64  | tmux gdb mailutils postfix lib32gcc1                             |