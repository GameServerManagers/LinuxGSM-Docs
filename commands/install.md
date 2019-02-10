# install

LinuxGSM allows for the simple installation of game servers. The installer is designed to get a game server to a working state allowing the game server to be started right away.

The installer will:

* Create required directories
* Install/advise on required dependencies
* Download the game server files
* Load config files
* Apply any fixes required to get the game server working

## Commands

### Standard Install

The standard installation is the default installation method that requires user interaction.

Standard: `./gameserver install`

Short: `./gameserver i`

### Auto Install

Auto install is useful for automatic server deployments as no user prompt is required.

Standard: `./gameserver auto-install`

Short: `./gameserver ai`

## Installation

1. Make your script executable:

`chmod +x gameserver`

2. Run the install command: `./gameserver install` or `./gameserver auto-install` to bypass any prompts.
3. Follow on screen instructions.

## Install Dependencies

Installation of dependencies requires either `sudo` or root access. LinuxGSM can automatically install dependencies if the user has `sudo` or is `root`.

{% hint style="warning" %}
If dependencies are not installed the server may not start.
{% endhint %}

### Dependencies as root

As `root` run `./gameserver install` and the installer will complete a dependency installation only, ignoring the other installation steps.

### Dependencies as sudo user

If a user has sudo access the installer will prompt to enter the sudo password to automatically install dependencies. If sudo is not available the installer will advise on the command required to install dependencies.

## Common Installation Issues

### User Permission Issues

LinuxGSM may fail to run if the correct permissions have not been used. This fault commonly occurs if an admin has not correctly followed installation instructions found on [https://linuxgsm.com](https://linuxgsm.com)

Common faults include:

* Trying to install the LinuxGSM as root.
* Trying to install LinuxGSM in a directory not owned by the correct user.
* Not making `gameserver` file executable using the `chmod +x` command.

If trying to run as `root` LinuxGSM will fail to run. See FAQ.

To check if the correct user owns the directory or `gameserver` file, use `ls -al`

**Example output**

```text
drwxrwxr-x  5 nmrihserver nmrihserver 4096 Jul 17 20:25 lgsm
drwxr-xr-x  4 nmrihserver nmrihserver 4096 Aug 27  2015 log
-rwxrwxr-x  1 nmrihserver nmrihserver 3885 Aug  9 23:04 nmrihserver
drwxrwxr-x  8 nmrihserver nmrihserver 4096 Jul 17 20:32 serverfiles
drwxrwxr-x  3 nmrihserver nmrihserver 4096 Jul 17 20:25 .steam
drwxrwxr-x  8 nmrihserver nmrihserver 4096 Aug 19 16:00 Steam
drwxrwxr-x  6 nmrihserver nmrihserver 4096 Aug 19 16:00 steamcmd
```

If some files/directories are not owned by the correct user, use the `chown` command. Login as `root` and use the following command, changing the details to match your server

`chown -R username:username /home/gameserver`

`chown -R csgoserver:csgoserver /home/csgoserver`

#### Poor Network Connection to Steam servers

If the connection to the Steam servers is poor \(quite common\), SteamCMD download can fail. This is why LinuxGSM will always ask you if installation was successful allowing admins to retry the download should it fail.

If there are still issues downloading try the [validate](validate.md) option.

`./gameserver validate`

If downloading is still failing it may be worth contacting your server provider to confirm steam servers are not being blocked for any reason.

It is also worth searching the internet for issues relating to the error message you receive.

### Not Enough Storage

Some game servers take up a significant amount of disk space. If you are having issues downloading check that your server has enough space available.

To check your available storage, use:

`df -h` or `./gameserver details`

### DNS Issue

Make sure you can `ping` using a hostname.

```text
ping google.com
```

Should this fail your server may not have DNS lookup correctly configured. [https://www.cyberciti.biz/faq/linux-setup-dns-lookup/](https://www.cyberciti.biz/faq/linux-setup-dns-lookup/)
