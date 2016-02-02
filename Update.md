# Updating your server

LGSM comes with an update functions. All Steam games are supported, as well as some other servers such as Teamspeak.


## Starting the automatic update process 

Just run : 

`./gameserver update`



## When an update isn't enough...

Sometimes, SteamCMD can mess up, either failing to download files properly, or missing some important files to update.
So if your server isn't starting after an update, or if it's still at the same server version, run the validate command.

`./gameserver validate`

Note that if you modified server core server files, they will be restored to their original version. But who does that ?
