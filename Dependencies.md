# Summary

> You can get more specific dependencies from the main website <a href="http://gameservermanagers.com/#supportedgames">http://gameservermanagers.com</a>.

Below is a complete list of dependencies required for all servers. Use your distros package manager (apt-get, yum etc) to install these requirements.

> These dependencies should be installed _before_ installing any LGSM server.

Select the engine/game you require.

### Engine/Game
* [Source Engine](#Source-Engine)
* [Gold Source Engine](#Gold-Source-Engine)
* [ARMA 3](#ARMA-3)
* [Just Cause 2](#Just-Cause-2)
* [Killing Floor/Red Orchestra](#Killing-Floor-Red-Orchestra)
* [Natural Selection 2/NS2: Combat](#Natural-Selection-2)
* [Project Zomboid](#Project-Zomboid)
* [Unreal Tournament 2004](#Unreal-Tournament-2004)
* [Unreal Tournament 99](#Unreal-Tournament-99)
* [SteamCMD](#SteamCMD)

# Notes
## Distro Compatibility
The older the server the less likely the game server will work on your server. For example _CentOS 5_ does not work with most servers. However _CentOS 6_ can but may require _glibc_ fixes.

### Recommended Distros
The below servers are the most compatible and work well with all servers.

* ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) => Ubuntu 12.04 LTS
* ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS 7
* ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian 8

Any distro with _=> GLIBC 2.15_ and _=> tmux 1.6_ will also be compatible with all servers.

### Glibc Compatibility

Different Servers have different Glibc requirements. For example _Counter Strike: Source_ requires _2.07_, whereas _Garry's Mod_ requires _2.15_.


If you are running an older distro check out the [[Glibc]] Wiki page.

## CentOS 6 EPEL
LGSM requires you install [EPEL](http://download.fedoraproject.org/pub/epel/6/i386/repoview/epel-release.html) if running CentOS 6.

This is because tmux is not available as a standard package in CentOS 6.

# <a name="Source-Engine"></a>Source Engine
Counter Strike: Global Offensive, Counter Strike: Source, Half Life 2:Deathmatch etc.

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS
| Distro        | Arch | Dependencies                                                       |
| ------------- | ---- | :----------------------------------------------------------------- |
| CentOS        | x32  | yum install tmux mailx postfix libstdc++                           |
| CentOS        | x64  | yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686 |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian
| Distro        | Arch | Dependencies                                                                                 |
| ------------- | ---- |:----------------------------------------------------------------                             |
| Debian        | x32  | apt-get install tmux mailutils postfix ca-certificates libstdc++6                            |
| Debian        | x64  | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386  |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu
| Distro           | Arch | Dependencies                                                                 |
| ---------------- | ---- |:---------------------------------------------------------------------------- |
| Ubuntu           | x32  | apt-get install tmux mailutils postfix libstdc++6                            |
| Ubuntu           | x64  | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386  |


## Other
| Distro           | Arch | Dependencies                   |
| ---------------- | ---- |:------------------------------ |
| Gentoo           | x32  | gdb mailutils postfix iproute2 |

# <a name="Gold-Source-Engine"></a>Gold Source Engine
Counter Strike 1.6, Deathmatch Classic etc.
## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS
| Distro        | Arch | Dependencies                      |
| ------------- | ---- | :-------------------------------- |
| CentOS        | x32  |  yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686 |
| CentOS        | x64  |  yum install tmux mailx postfix libstdc++  |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian
| Distro        | Arch | Dependencies                                         |
| ------------- | ---- |:---------------------------------------------------- |
| Debian        | x32  | apt-get install tmux mailutils postfix ca-certificates libstdc++6            |
| Debian        | x64  | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386 |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu
| Distro           | Arch | Dependencies                                                     |
| ---------------- | ---- |:---------------------------------------------------------------- |
| Ubuntu | x32  | apt-get install tmux mailutils postfix libstdc++6                                        |
| Ubuntu | x64  | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386                              |

<a name="ARMA-3"></a>ARMA 3
------

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS

| Distro | Arch | Dependencies                                     |
|----------|--------|----------------------------------------------|
| CentOS | x32    |  yum install tmux mailx postfix libstdc++                      |
| CentOS | x64    |  yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686                 |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian

| Distro | Arch | Dependencies                                                         |
|----------|--------|------------------------------------------------------------------|
| Debian | x32    | apt-get install tmux mailutils postfix ca-certificates libstdc++6                 |
| Debian | x64    | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386  |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu

| Distro         | Arch | Dependencies                                         |
|------------------|--------|--------------------------------------------------|
| Ubuntu  | x32    | apt-get install tmux mailutils postfix libstdc++6                 |
| Ubuntu  | x64    | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386  |

<a name="Just-Cause-2"></a>Just Cause 2
------------

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS

| Distro | Arch | Dependencies                                     |
|----------|--------|----------------------------------------------|
| CentOS | x32    | yum install tmux mailx postfix libstdc++              |
| CentOS | x64    | yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686  |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian

| Distro | Arch | Dependencies                                                         |
|----------|--------|------------------------------------------------------------------|
| Debian | x32    | apt-get install tmux mailutils postfix ca-certificates libstdc++6  |
| Debian | x64    | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386  |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu

|   Distro         | Arch | Dependencies                                       |
|------------------|--------|--------------------------------------------------|
| Ubuntu  | x32    | apt-get install tmux mailutils postfix libstdc++6                 |
| Ubuntu | x64    | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386 |

<a name="Killing-Floor-Red-Orchestra"></a>Killing Floor/Red Orchestra
---------------------------

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS

|   Distro |   Arch |   Dependencies                               |
|----------|--------|----------------------------------------------|
| CentOS | x32    |  yum install tmux mailx postfix libstdc++                 |
| CentOS | x64    |  yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686  |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian

|   Distro |   Arch |   Dependencies                                   |
|----------|--------|--------------------------------------------------|
| Debian | x32    | apt-get install tmux mailutils postfix ca-certificates libstdc++6            |
| Debian | x64    | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386  |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu

| Distro           | Arch   | Dependencies                     |
|------------------|--------|----------------------------------|
| Ubuntu  | x32    | apt-get install tmux mailutils postfix libstdc++6            |
| Ubuntu  | x64    | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386  |

<a name="Natural-Selection-2"></a>Natural Selection 2/ NS2: Combat (Spark)
-------------------

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS

| Distro | Arch | Dependencies                                  |
|----------|--------|-------------------------------------------------|
| CentOS | x32    | yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686 speex.i686 tbb.i686 |
| CentOS | x64    | yum install tmux mailx postfix libstdc++ speex tbb |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian

| Distro | Arch | Dependencies                                                               |
|----------|--------|------------------------------------------------------------------------------|
| Debian | x32    | apt-get install tmux mailutils postfix ca-certificates libstdc++6 speex libtbb2           |
| Debian | x64    | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386 speex:i386 libtbb2 |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu

| Distro         | Arch | Dependencies                                                               |
|------------------|--------|------------------------------------------------------------------------------|
| Ubuntu | x32    | apt-get install tmux mailutils postfix libstdc++6 speex libtbb2 |
| Ubuntu | x64    | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386 speex:i386 libtbb2 |

<a name="Project-Zomboid"></a>Project Zomboid
---------------------------------------------

> note: Dependancies not yet confirmed.

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS

| Distro | Arch | Dependencies                                        |
|----------|--------|-------------------------------------------------|
| CentOS | x32    |  yum install tmux mailx postfix libstdc++ java-1.7.0-openjdk  |
| CentOS | x64    |   yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686 java-1.7.0-openjdk  |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian

| Distro   | Arch   | Dependencies                                                                 |
|----------|--------|------------------------------------------------------------------------------|
| Debian | x32    |  apt-get install tmux mailutils postfix ca-certificates libstdc++6 default-jre |
| Debian | x64    | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386 default-jre |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu

| Distro           | Arch   | Dependencies                                                       |
|------------------|--------|----------------------------------------------------------------|
| Ubuntu | x32    | apt-get install tmux mailutils postfix libstdc++6 default-jre  |
| Ubuntu | x64    | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386 default-jre   |

<a name="Unreal-Tournament-2004"></a>Unreal Tournament 2004
----------------------

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS

| Distro | Arch | Dependencies                                                        |
|----------|--------|-----------------------------------------------------------------------|
| CentOS | x32    | yum install tmux mailx postfix libstdc++ compat-libstdc++-33 SDL      |
| CentOS | x64    | yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686 compat-libstdc++-33.i686 SDL.i686 |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian

| Distro | Arch | Dependencies                                                      |
|----------|--------|--------------------------------------------------------------------|
| Debian | x32    | apt-get install tmux mailutils postfix ca-certificates libstdc++6 libsdl1.2debian  libstdc++5 |
| Debian | x64    | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386 libsdl1.2debian libstdc++5:i386 |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu

| Distro         | Arch | Dependencies                               |
|------------------|--------|----------------------------------------------|
| Ubuntu | x32    | apt-get install tmux mailutils postfix libstdc++6 libsdl1.2debian libstdc++5      |
| Ubuntu | x64    | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386 libsdl1.2debian libstdc++5:i386 |

<a name="Unreal-Tournament-99"></a>Unreal Tournament 99
--------------------

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS

| Distro | Arch | Dependencies                          |
|----------|--------|-----------------------------------------|
| CentOS | x32    |  yum install tmux mailx postfix libstdc++ SDL |
| CentOS | x64    | yum install tmux mailx postfix glibc.i686 libstdc++ libstdc++.i686 SDL.i686 |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian

| Distro | Arch | Dependencies                                         |
|----------|--------|--------------------------------------------------------|
| Debian | x32    | apt-get install tmux mailutils postfix ca-certificates libstdc++6 libsdl1.2debian |
| Debian | x64    | apt-get install tmux mailutils postfix ca-certificates lib32gcc1 libstdc++6 libstdc++6:i386 libsdl1.2debian |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu

| Distro         | Arch | Dependencies                         |
|------------------|--------|----------------------------------------|
| Ubuntu | x32    | apt-get install tmux mailutils postfix libstdc++6 libsdl1.2debian |
| Ubuntu | x64    | apt-get install tmux mailutils postfix lib32gcc1 libstdc++6 libstdc++6:i386 libsdl1.2debian |


<a name="SteamCMD"></a>SteamCMD
--------

Requirements for [SteamCMD] only. SteamCMD is a 32-bit application and requires extra packages to work on 64-bit distros. These packages are already included with the game server requirements.

## ![CentOS Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/centos-icon-32.png) CentOS

| Distro | Arch | Dependencies                |
|----------|--------|-------------------------|
| CentOS | x32    | glibc libstdc++           |
| CentOS | x64    | glibc.i686 libstdc++.i686 |

## ![Debian Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/debian-icon-32.png) Debian

| Distro | Arch | Dependencies |
|----------|--------|----------------|
| Debian | x32    | apt-get install libstdc++6 |
| Debian | x64    | apt-get install lib32gcc1 libstdc++6 libstdc++6:i386 |

## ![Ubuntu Icon](https://github.com/dgibbs64/linuxgsm/blob/master/images/icons/ubuntu-icon-32.png) Ubuntu

| Distro | Arch   | Dependencies |
|--------|--------|----------------|
| Ubuntu | x32    | apt-get install libstdc++6 |
| Ubuntu | x64    | apt-get install lib32gcc1 libstdc++6 libstdc++6:i386 |