# FAQ

Below is a list of common questions that people ask about the Linux Game Server Managers.

FAQ section is to try to help with common problems with LinuxGSM.

## I'm having an issue can you help?

There are various ways to get help and support with LinuxGSM.

* [http://linuxgsm.com/support](https://linuxgsm.com/support)

{% hint style="warning" %}
Remember to consider the best place to post your issue and search the internet for a solution before posting.
{% endhint %}

### Documentation

The website and GitHub wiki is a useful resource for various LinuxGSM related topics.

* [https://linuxgsm.com](https://linuxgsm.com)
* [https://docs.linuxgsm.com](https://docs.linuxgsm.com)

### General Support

LinuxGSM has a discord server where you can get general support for LinuxGSM related stuff.

* [https://linuxgsm.com/discord](https://linuxgsm.com/discord)

### Bugs/Feature Requests

LinuxGSM has a GitHub issues page where you can submit any bugs and feature suggestions.

* [https://linuxgsm.com/issues](https://linuxgsm.com/issues)

## tmux: command not found

I received the following error

```
[ FAIL ] Tmux not installed
    * Tmux is required to run this server.
        * Please see the the following link.
        * http://linuxgsm.com/tmux
```

Tmux has not been installed. See the dependencies section of the installation instructions.

```
apt-get install tmux
```

or

```
yum install tmux
```

## Can I run a server as root?

```
[ FAIL ] Script will not run as root!
```

The script will not run as root and will error if you try. This is done for the following good reasons:

* So you or someone else don't accidentally damage your system. (`rm -rf *` anyone?).
* So you don't mess up your game servers user permissions.
* To help prevent someone potentially using your game server and gain root access.
* Keeping the game server compartmentalised in its own directory away from your other stuff.
* Its really bad practice to run scripts as root.
* Would you really trust yourself as root after a 9 hour energy-drink fuelled CS:GO session?
* Did i mention so you don't break everything!?

## I can't download linuxgsm.sh (TLS/SSL Errors)

If your error looks like `Unable to establish SSL connection` you need to make sure you installed the `ca-certificates` package first as well as other dependencies showed on the website's documentation.

If you are using an "old" distribution, it is possible that your version of wget doesn't support redirects along with SSL/TLS. As a workaround, you can download the script using `--no-check-certificate`. Please note that you should only tolerate this practice if your trust your server network connection and the download source at 100%.

```
wget -N --no-check-certificate https://linuxgsm.sh
```

## How can I install \[insert name] mod?

LinuxGSM installs a vanilla server by default. There is now a mods-install feature with a limited selection of popular mods. All other mods will have to be install manually. It is recommend you visit the official add-on/mod installation guides for more info.

Here are a few useful resources for this.

* [Metamod: Source](http://www.sourcemm.net/)
* [Metamod](http://metamod.org/)
* [Sourcemod](http://www.sourcemod.net/)
* [AMX Mod X](http://www.amxmodx.org/)
* [Alliedmodders](http://alliedmods.net/)

## Will LinuxGSM run on Raspberry PI?

Short answer: No

Raspberry PI uses ARM architecture whereas all the game servers will only run on x86 compatible architectures such as 32-bit and 64-bit versions of distros. Raspberry PI is not compatible with x86.

## Can I bind game servers to a given CPU core?

Short answer: You should not.

Experience proves Linux's embed CPU scheduler to work the best: Each server will freely use available CPU time, spread across multiple cores/threads in order to prevent adjacent processes from slowing down each other. This allows for equitable resources distribution for all processes; in the case of CPU saturation, all processes will be slowed down by just a bit. On the other hand, binding processes to CPU cores usually provides zero to low performance gains, while causing various issues including performance loss, most of the time for the following reason: A process that is not bound to specific CPU cores uses the core you bound your game server to, which slows it down more than if CPU usage was spread across the whole CPU.

## Will LinuxGSM run on Linux for Windows?

Short answer: Yes.

A new feature in Windows 10 called **WSL2** was released allowing the installation of some Linux Distros in to Windows. WSL initially did not work as it did not support i386 binary's however with WSL2 it works. So you can now run LInuxGSM on your Windows 10 PC.

For more info see this useful video on the subject.

{% embed url="https://www.youtube.com/watch?v=loC7VfgRT-I" %}



## \[ WARN ] Multiple active network interfaces.

You will get the following message if your server has multiple IP addresses. The game server can only bind to one IP address, because of this you need to tell the server which IP address you want to use.

```
[ WARN ] Multiple active network interfaces

Manually specify the IP you want to use within the csgoserver script.
Set ip="0.0.0.0" to one of the following:
127.0.0.2
162.252.9.37
162.252.9.39
162.252.9.41
```

Edit the LinuxGSM config located in lgsm/config-lgsm/\[servername]/

Find and edit the following line and change it to the IP address you want to use.

```
ip="0.0.0.0"
```

## version \`GLIBC\_2.15′ not found

```
version `GLIBC_2.15′ not found
```

The correct version of Glibc is not installed. See the dependencies section of the installation instructions.

## write error: No space left on device

```
write error: No space left on device
```

The script cannot write to the server because there is no disk space available on your server. Free up some space to resolve.

## Can you create a server script for a \[insert name] game server?

You can request a script is created for a particular server by submitting a feature request on the \[GitHub issues] page. This does not guarantee it will be created but we will review it and decide if its possible and how much demand there is for it. Servers will be created when time permits.

Please also check that the server can run on Linux before submitting. Servers that require WINE will not be considered. You can use SteamDB.info to find the server and check Linux comparability.

If you have an interest in developing with BASH then you are also welcome to contribute and develop a game server in to LinuxGSM.

## Can you remote on to my server and help me set up my game server?

In general we do not remote on to users servers, unless it is to assist in development.

## I found a bug how do I report it?

If you find a bug or have a suggestion please submit a bug report on [GitHub issues](https://github.com/dgibbs64/linuxgsm/issues) page.

## How can I install a non-steam version?

Non-steam versions of the games ARE pirated and this would be the only reason to use non-steam versions. Simply purchase the game via steam. Steam has two massive sales a year with 75% of most of there titles there is really no excuse for pirating these games. [http://steampowered.com](http://steampowered.com)

## What server do I need?

LinuxGSM itself has extremely low server requirements as it is written in BASH. However the game servers themselves do have hardware requirements. You need to be aware of these requirements in order to choose a server that fits your needs. There are no hard and fast rules when is comes to server requirements and depends upon many factors.

* Hard Disk: You will need to ensure you have enough disk space to install the game server. The space required varies drastically depending upon the game. Generally the older the game the smaller the size. If the server is on SteamCMD you can use SteamDB to find out the disk requirements. For example [https://steamdb.info/app/403240/depots/](https://steamdb.info/app/403240/depots/). Also taken in to consideration any mods, addons, backups etc you might need.
* CPU: Most game servers are mono threaded. This means it will only use one CPU core per instance, because of this it is worth looking at performance of an individual core. Every game server has different resource requirements with certain factors increasing CPU demand. For example, In Rust the map size greatly effects CPU usage. For Counter-Strike the tickrate and bots will make a difference. Whereas for Garry's Mod the number of connected players, addons, and props that are used and spawned increase server requirements.
* RAM: Again the specific game server will impact upon the RAM requirements. In general factors such as map size number of players, bots, addons can have an impact on the RAM required. For example a No More Room in Hell server has a much lower RAM requirement than ARK or Rust. The game engine also plays a massive role in RAM requirements, with Rust using aroumd 12GB and ARK using around 6GB, Unity3D engine games can also have higher requirements.
* Network: Game servers are not usually very demanding in terms of bandwidth. However, the connection must be reliable and consistent to ensure players get a good experience. Reducing ping and packet loss is very important, otherwise players will experience latency and lag. Your servers location has a big effect on ping, so try to get your server relatively close to where your players are going to be. If your players are in France then a server in Europe is going to be much better than one in the US for example. Servers can sometimes come under attack so DDoS protection is also important.

## I'm getting 404 errors when running functions

You're lacking the required function, because you didn't run this command before the last huge LinuxGSM update. The function structure changed, that's why you're getting a 404 error. You just need the newer LinuxGSM version.

```
./gameserver update-lgsm
```

## \[ FAIL ] Starting game-server: Ownership issues found

The user that you are running LinuxGSM with does not own all of its files.

More information, see [Ownership](../linux/file-ownership.md)

**Getting rid of bad practice**

**Case 1)** You've been uploading files as root or any other user than your gameserver user. If you're logging into your FTP as root, you must know that this is wrong on so many levels and must consider using a better method urgently. Here is an [example](https://gist.github.com/UltimateByte/229c17b3c48ca10080c5e56b5513e476) of a simple user based FTP set in 2 minutes with proftpd which would already be better. Otherwise, one way better practice is to use SFTP that comes with SSH. No need to install an FTP server as long as you've got an SSH server. Just setup your FTP client to use SFTP, and connect with the same port as your SSH server and with your username/password.

**Case 2)** You've been downloading/extracting/copying files as root instead of the appropriate user. Just don't, do it as the user, OR, if you're obstinate, then at least chown files afterwards.

**Fixing wrong ownership**

You can simply fix those ownership issues by using a chown command as root.

```
chown -R username:username /home/username
```

## \[ FAIL ] Starting game-server: Permission issues found

It usually means some script or executable files are not actually executable.

Useful command:

```
chmod +x <filename>
```

To learn more about this, see [Permissions](../linux/permissions.md)

## My server is not showing up over LAN or Internet

This can have numerous reasons. Here are some ways do diagnose this issue:

* Check your game logs to see if it contains any clue
* Is your server listening? Input `./gameserver details` to get the corresponding command to know it
* Are you behind [Firewalls](../linux/firewalls.md)? Double check your rules, try to disable it for testing
* Do you have multiple interface? Set the right IP within your "gameserver" script or the game config file
* Is it a home server? If you're behind a router, make sure your're listening to your local IP, then redirect appropriate ports to this local IP within your router settings.
* Are the ports you're using free? See [Ports](../configuration/ports.md)
* Did you wait long enough? Sometimes it's just a matter of time until your server shows up into the list

## How do I  solve a  segmentation fault?

My source server is displaying an error like `./srcds_run: line 318: 31093 Segmentation fault`

This kind of errors can happen at any time or be due to numerous reasons. However, most common ones are:

If it happens upon start:

* Interpreter issue (glibc libstdc gcc libraries and so on) - check your versions, libraries, and game binary files.
* Outdated or bugged addon - Update or remove the addon
* Missing or revoked GSLT - Update your GSLT
* Corrupted game server files - run ./gameserver validate
* File version incompatibility - run ./gameserver validate

If it happens after a while:

* Bug from the game server or an addon - Check your console logs, see if you can reproduce, and diagnose your addons
* Unstable hardware - very unlikely, check your system stability
* Ulimit issue: Your system cannot open as many files as it should - See ulimit info from this page

## How do I change the LinuxGSM branch?

To change the LinuxGSM branch from the default `master` edit the LinuxGSM executable file.

either `linuxgsm.sh` or `gameserver` e.g `csgoserver`

edit the following lines as required.

```
## GitHub Branch Select
# Allows for the use of different function files
# from a different repo and/or branch.
githubuser="GameServerManagers"
githubrepo="LinuxGSM"
githubbranch="master"

```

Once the details are changed update LinuxGSM.

```
./gameserver update-lgsm
```
