# Updating your server

LinuxGSM comes with an update server feature. All SteamCMD games servers are supported, as well as some other servers such as Teamspeak.


## Commands

`./gameserver update`  
`./gameserver u`

Note: If there is no update available, your server won't be restarted.

## Automatic update

### Update on start

You can update your server on start, by editing your game main script.

`updateonstart="on"`

This has the inconvenience of making your server longer to start but can be useful for servers that are kept off most of the time such as match servers.

### Scheduled updates

Using cronjobs, you can set a cronjob to run the update function at any given time.
LGSM team advise you to use root cronjobs. Just login as root, then edit your cronjobs. 

To edit your cronjobs, type : 

`crontab -e`

Here is an example of a user based cronjob for daily update at 5am (replace the username and gameserver according to your case) : 

`0 5 * * *  /home/username/gameserver update > /dev/null 2>&1`

Here is an example of a root based cronjob for daily update at 5am : 

`0 5 * * *  su - username -c '/home/username/gameserver update' > /dev/null 2>&1`



## When an update isn't enough...

Sometimes, SteamCMD can mess up, either failing to download files properly, or missing some important files to update.
So if your server isn't starting after an update, or if it's still at the same server version, run the validate command.

`./gameserver validate`  
`./gameserver v`

Note: if you modified core server files, they will be restored to their original version. But who does that anyway ?



# Updating your LGSM script
LGSM has the ability to self update functions.

## update-functions

`./gameserver update-functions`  
`./gameserver uf`