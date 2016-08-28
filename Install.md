# Installing your server

LGSM provides an automatic installer for every game server. The installer will be the first thing you run when getting started with your server.

1. Make your script executable: 

`chmod +x gameserver`

2. Run the install command:

`./gameserver install`

Now simply follow instructions !
And voilà !


## Failing installations

### Permissions issues

Did you make a dedicated user for that server? Is your current directory owned by that user? Did you `chmod +x` the script?

Make sure the directory you are installing your game in actually belongs to the right user: 

`ls -al`

Example

	drwxrwxr-x  5 nmrihserver nmrihserver 4096 Jul 17 20:25 lgsm
	drwxr-xr-x  4 nmrihserver nmrihserver 4096 Aug 27  2015 log
	-rwxrwxr-x  1 nmrihserver nmrihserver 3885 Aug  9 23:04 nmrihserver
	drwxrwxr-x  8 nmrihserver nmrihserver 4096 Jul 17 20:32 serverfiles
	drwxrwxr-x  3 nmrihserver nmrihserver 4096 Jul 17 20:25 .steam
	drwxrwxr-x  8 nmrihserver nmrihserver 4096 Aug 19 16:00 Steam
	drwxrwxr-x  6 nmrihserver nmrihserver 4096 Aug 19 16:00 steamcmd


If not, use some chown commands. Login to root, then run this command, replacing "username" by your actual username : 

`chown -R username:username /home/username`

### Bad network to Steam servers

If your connection to Steam servers is bad (which is very common...), SteamCMD download can fail. That's why LGSM will always ask you if installation was successful to retry it if needed. If you have trouble getting it done, you can try :  

`./gameserver validate`

### Missing packages

You may not of installed all the required dependencies to run the server.
Go on the desired server page of [http://gameservermanagers.com/](http://gameservermanagers.com/), then select your distro, to know all packages you need to install.

### Not enough disk space
Check your remaining disk space.
To check your disk remaining space, use: 

`df -h` or `./gameserver details

### DNS Issue

Did you configure your DNS properly ? Installer can't work without access to DNS.