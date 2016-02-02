# Installing your server

LGSM provides an automatic installer for every Steam game servers, and many others. This is the first thing you're probably gonna do after getting your LGSM script.

First, make sure that your script is executable : 

`chmod +x gameserver`

Then run the install command :

`./gameserver install`

Then follow instructions !
And voilà !


## Failing installations

### Bad network to Steam servers

If your connection to Steam servers is bad (which is very common...), SteamCMD download can fail. That's why LGSM will always ask you if installation was successful to retry it if needed. If you have trouble getting it done, you can try :  

`./gameserver validate`

### Missing packages

Some of your don't install packages properly. You're gonna have some trouble. Install them. Just do it.
Go on the desired server page of [http://gameservermanagers.com/](http://gameservermanagers.com/), then select your distro, and install all required packages.

### Not enough disk space
This title is pretty self explanatory, check your remaining disk space.
To check your disk remaining space, use : 

`df -h`

Also, make sure the folder you're installing your game in actually belongs to the right user : 

`ls -al`

If not, use some chown commands. Login to root, then run those commands, replacing "username" by your actual username : 

`cd /home`

`chown -R username:username username`