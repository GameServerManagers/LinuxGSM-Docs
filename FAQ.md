Below is a list of common questions that people ask about the Linux Game Server Managers.

FAQ section is to try to help with common problems with LGSM.

I'm having an issue can you help?
===============================================

We do want to help you with errors and issues you are having. However please only post an issue if you an issue with LGSM itself.

**LGSM Scripts:** Yes we can provide assistance with LGSM related issues. This maybe such things as an error LGSM is returning or not doing what it is meant to do. Most common problem is that there is a bug in the code that needs to be resolved.

**Game Server:** No we cannot provide assistance with game server related issues. This is because we did not create the game server and have no control of how the game server is developed. This was created by the developer of the game e.g Valve, Facepunch, Tripwire etc. We recommend you seek support from the Games official forums etc. or someone of the the LGSM Steam Group may be able to help  

**Server distro/OS:** No we cannot provide assistance with your servers distro. This is because we did not create the distro. This was created by the developer of the distro e.g Ubuntu, Debian, CentOS etc. You should seek support from the distros official forums etc.

**Unsure what the issue is related to?** If the issue is being generated in debug mode or the console it is likely a game server or distro related issue. 

Remember posting an issue in the correct forum etc. will help you resolve your issue quickly and allows developers to spend more time on issues we can actually assist with.

tmux: command not found
=======================

I received the following error

    [ FAIL ] Tmux not installed
        * Tmux is required to run this server.
            * Please see the the following link.
            * http://gameservermanagers.com/tmux

OR

    tmux: command not found

Tmux has not been installed. See the dependencies section of the instructions.

    apt-get install tmux

or

    yum install tmux

Can I run a server as root?
===========================
The script will not run as root and will error if you try. This is for security and to stop permissions issues. For example, if you run update as root any changed files are then owned by root. This means the arma3server user will be unable to access the updated files causing the server to fail.

    [ FAIL ] Script will not run as root!

How can I install [insert name] mod?
====================================
I have no idea….Why not go and check out the mods official website for install instructions?

Here are a few useful resources for this.
* [Metamod: Source](http://www.sourcemm.net/)
* [Metamod](http://metamod.org/)
* [Sourcemod](http://www.sourcemod.net/)
* [AMX Mod X](http://www.amxmodx.org/)
* [Alliedmodders](http://alliedmods.net/)

Will LGSM run on Raspberry PI?
==============================
Short answer: No

Raspberry PI uses ARM architecture whereas all the game servers will only run on x86 compatible architectures such as 32-bit and 64-bit versions of distros. Raspberry PI is not compatible with x86.

[ WARN ] Multiple active network interfaces.
============================================

You will get the following message if your server has multiple IP addresses. The game server can only bind to one IP address, because of this you need to tell the server which IP address you want to use.

    [ WARN ] Multiple active network interfaces

    Manually specify the IP you want to use within the csgoserver script.
    Set ip="0.0.0.0" to one of the following:
    127.0.0.2
    162.252.9.37
    162.252.9.39
    162.252.9.41

Edit the script file

    vi csgoserver

Find and edit the following line and change it to the IP address you want to use.

    ip="0.0.0.0"

version \`GLIBC\_2.15′ not found
================================

    version `GLIBC_2.15′ not found

The correct version of Glibc is not installed. See the [dependencies][] section of the instructions.

write error: No space left on device
====================================

    write error: No space left on device

The script cannot write to the server because there is no disk space available on your server. Free up some space to resolve.

ulimit SteamCMD startup error
=============================

    ./steamcmd.sh: line 17: ulimit: open files: cannot modify limit: Operation not permitted

Some users may get a ulimit error (no permission/cannot open file) while script is starting up. This error caused by a low setting of the -n parameter (number of file descriptors) of ulimit. Some servers forbid increasing ulimit values after startup (or beyond a limit set by root).
This can be fixed by changing the file descriptor number ulimit:

    ulimit -n 2048

Can you create a server script for a [insert name] game server?
===============================================================

You can request I create a script for a particular server by submitting a feature request on the [GitHub issues] page. This does not guarantee I will create a script but I will review it and decide if its possible and how much demand there is for it. Servers will be created when time permits.

Please also check that the server can run on Linux before submitting. Servers that require WINE will not be considered.

Can you remote on to my server and help me set up my game server?
=================================================================
No! That takes all the fun out of it for you and I am not free tech support.

I found a bug how do I report it?
=================================

If you find a bug or have a suggestion please submit a bug report on [GitHub issues][] page.

<https://github.com/dgibbs64/linuxgameservers/issues>

How can I install a non-steam version?
======================================

Non-steam versions of the games ARE pirated and this would be the only reason to use non-steam versions. Simply purchase the game via steam. Steam has two massive sales a year with 75% of most of there titles there is really no excuse for pirating these games. <http://steampowered.com>

[S\_API FAIL] SteamAPI\_Init() failed; SteamAPI\_IsSteamRunning() failed.
=========================================================================

Ignore the error, do not do anything to attempt to fix it. It is a known issue that has been happening ever since SteamPipe was introduced (this includes on Source1 games). It does not cause any issue and can be freely ignored.

  [dependencies]: dependencies "wikilink"
  [GitHub issues]: https://github.com/dgibbs64/linuxgameservers/issues