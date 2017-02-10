Below is a list of common questions that people ask about the Linux Game Server Managers.

FAQ section is to try to help with common problems with LGSM.

I'm having an issue can you help?
===============================================

There are various ways to get help and support with LGSM.
* http://gameservermanagers.com/support/

_Remember to consider the best place to post your issue and search the internet for a solution before posting._

## Documentation
The website and GitHub wiki is a useful resource for various LGSM related topics.
* http://gameservermanagers.com
* http://gameservermanagers.com/wiki

## General Support
LGSM has a Steam Group where you can get general support for LGSM related stuff.
* http://gameservermanagers.com/steam

## Bugs/Feature Requests
LGSM has a GitHub issues page where you can submit any bugs and feature suggestions.
* http://gameservermanagers.com/issues

tmux: command not found
=======================

I received the following error

    [ FAIL ] Tmux not installed
        * Tmux is required to run this server.
            * Please see the the following link.
            * http://gameservermanagers.com/tmux

Tmux has not been installed. 
See the dependencies section of the installation instructions.

    apt-get install tmux

or

    yum install tmux

Can I run a server as root?
===========================

    [ FAIL ] Script will not run as root!

The script will not run as root and will error if you try. This is done for the following good reasons:
* So you or someone else don't accidentally damage your system. (rm -rf * anyone?).
* So you don't mess up your game servers user permissions.
* To help prevent someone potentially using your game server and gain root access (stealing your internets and stuff!).
* Keeping the game server compartmentalised in its own directory away from your other stuff.
* Its really bad practice to run scripts as root.
* Would you really trust yourself as root after a 9 hour energy-drink fueled CS:GO session?
* Did i mention so you don't break everything!?

![](http://truegif.com/pictures/gif/9281.gif)

How can I install [insert name] mod?
====================================
LGSM installs a vanilla server by default. You can customise your server however you want. I reccomend you checkout add-on/mod installation guide.

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

The correct version of Glibc is not installed.
See the dependencies section of the installation instructions.

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

You can request a script is created for a particular server by submitting a feature request on the [GitHub issues] page. This does not guarantee it will be created but we will review it and decide if its possible and how much demand there is for it. Servers will be created when time permits.

Please also check that the server can run on Linux before submitting. Servers that require WINE will not be considered.

Can you remote on to my server and help me set up my game server?
=================================================================
No! That takes all the fun out of it for you and I am not free tech support.

I found a bug how do I report it?
=================================

If you find a bug or have a suggestion please submit a bug report on [GitHub issues][] page.

<https://github.com/dgibbs64/linuxgsm/issues>

How can I install a non-steam version?
======================================

Non-steam versions of the games ARE pirated and this would be the only reason to use non-steam versions. Simply purchase the game via steam. Steam has two massive sales a year with 75% of most of there titles there is really no excuse for pirating these games. <http://steampowered.com>

[S\_API FAIL] SteamAPI\_Init() failed; SteamAPI\_IsSteamRunning() failed.
=========================================================================

Ignore the error, do not do anything to attempt to fix it. It is a known issue that has been happening ever since SteamPipe was introduced (this includes on Source1 games). It does not cause any issue and can be freely ignored.

  [GitHub issues]: https://github.com/dgibbs64/linuxgsm/issues

I'm getting 404 errors when running functions
=========================================================================

You're lacking the required function, because you didn't run this command before the last huge LGSM update. The function structure changed, that's why you're getting a 404 error. You just need the newer LGSM version.

`./gameserver update-functions`

[ FAIL ] Starting game-server: Ownership issues found
=========================================================================

The user that you're running LGSM with doesn't own all of its files.

More information, see [Ownership](https://github.com/GameServerManagers/LinuxGSM/wiki/File-Ownership)

**Getting rid of bad practice**

**Case 1)** You've been uploading files as root or any other user than your gameserver user. If you're logging into your FTP as root, you must know that this is wrong on so many levels and must consider using a better method urgently. Here is an [example](https://gist.github.com/UltimateByte/229c17b3c48ca10080c5e56b5513e476) of a simple user based FTP set in 2 minutes with proftpd which would already be better. Otherwise, one way better practice is to use SFTP that comes with SSH. No need to install an FTP server as long as you've got an SSH server. Just setup your FTP client to use SFTP, and connect with the same port as your SSH server and with your username/password.

**Case 2)** You've been downloading/extracting/copying files as root instead of the appropriate user. Just don't, do it as the user, OR, if you're obstinate, then at least chown files afterwards.

**Fixing wrong ownership**

You can simply fix those ownership issues by using a chown command as root.

`chown -R username:username /home/username`

[ FAIL ] Starting game-server: Permission issues found
=========================================================================

It usually means some script or executable files are not actually executable.

Useful command: 

`chmod +x <filename>`

To learn more about this, see [Permissions](https://github.com/GameServerManagers/LinuxGSM/wiki/Permissions)


My server is not showing up over LAN or Internet
=========================================================================

This can have numerous reasons. Here are some ways do diagnose this issue:

* Check your game logs to see if it contains any clue
* Is your server listening? Input `./gameserver details` to get the corresponding command to know it  
* Are you behind [[Firewalls]]? Double check your rules, try to disable it for testing
* Do you have multiple interface? Set the right IP within your "gameserver" script or the game config file
* Is it a home server? If you're behind a router, make sure your're listening to your local IP, then redirect appropriate ports to this local IP within your router settings.
* Are the ports you're using free? See [[Ports]]
* Did you wait long enough? Sometimes it's just a matter of time until your server shows up into the list

Segmentation fault
=========================================================================

My source server is displaying an error like  
`./srcds_run: line 318: 31093 Segmentation fault `

This kind of errors can happen at any time or be due to numerous reasons. However, most common ones are:

If it happens upon start:  
* Interpreter issue (glibc libstdc gcc libraries and so on) - check your versions, librarires, and game binary files.
* Outdated or bugged addon - Update or remove the addon
* Missing or revoked GSLT - Update your GSLT
* Corrupted game server files - run ./gameserver validate
* File version incompatibility - run ./gameserver validate

If it happens after a while:  
* Bug from the game server or an addon - Check your console logs, see if you can reproduce, and diagnose your addons
* Unstable hardware - very unlikely, check your system stability
* Ulimit issue: Your system cannot open as many files as it should - See ulimit info from this page