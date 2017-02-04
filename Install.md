One of the main advantages for LinuxGSM is that will install the game server for the admin. The installer will be the first thing an admin will run when getting started with a server.

# Installation

1. Make your script executable: 

`chmod +x gameserver`

2. Run the install command:

`./gameserver install`

3. Follow on screen instructions
And voilà !

# Common installation issues

## Permissions issues

LinuxGSM may fail to run if the correct permissions have not been used. This fault commonly occurs if an admin has not correctly followed installation instructions found on https://gameservermanagers.com

Common faults include:
* trying to install the LinuxGSM as root. 
* Trying to install LinuxGSM in a directory not owned by the correct user
* not making `gameserver` file executable using the `chmod +x` command.

if you try to run as root LinuxGSM will fail to run. See [FAQ](https://github.com/GameServerManagers/LinuxGSM/wiki/FAQ#can-i-run-a-server-as-root)

To check the correct user owns the directory or `gameserver` file use `ls -al`

**Example output**

	drwxrwxr-x  5 nmrihserver nmrihserver 4096 Jul 17 20:25 lgsm
	drwxr-xr-x  4 nmrihserver nmrihserver 4096 Aug 27  2015 log
	-rwxrwxr-x  1 nmrihserver nmrihserver 3885 Aug  9 23:04 nmrihserver
	drwxrwxr-x  8 nmrihserver nmrihserver 4096 Jul 17 20:32 serverfiles
	drwxrwxr-x  3 nmrihserver nmrihserver 4096 Jul 17 20:25 .steam
	drwxrwxr-x  8 nmrihserver nmrihserver 4096 Aug 19 16:00 Steam
	drwxrwxr-x  6 nmrihserver nmrihserver 4096 Aug 19 16:00 steamcmd


If some files/directorys are not owned use the `chown` command to correct this. 
Login as root and use the following command; changing the details to match your server

`chown -R username:username /home/gameserver`

`chown -R csgoserver:csgoserver /home/csgoserver`

### Bad network to Steam servers

If your connection to the Steam servers are bad (quite common), SteamCMD download can fail. This is why LinuxGSM will always ask you if installation was successful allowing admins to retry the download if it fails. 

If you you are having issues downloading try the [[validate]] option.

`./gameserver validate`

If downloading is still failing it may be worth contacting your server provider to confirm steam servers are not being blocked for any reason.

It is also worth searching the internet for issues relating to the error message you receive.

## Not enough disk space
Some game servers do use significant disk space. If you are having issues downloading check that your server has enough space available

To check your disk remaining space, use: 

`df -h` or `./gameserver details

### DNS Issue

Make sure you can `ping` web addresses

`ping google.com`

should this fail your server may not have DNS lookup correctly configured.
https://www.cyberciti.biz/faq/linux-setup-dns-lookup/