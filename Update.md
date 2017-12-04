LinuxGSM comes with an game server `update` command. All SteamCMD games servers are supported, as well as some other servers such as Teamspeak, Minecraft, Mumble & Factorio.

# Commands

Standard: `./gameserver update`

Short: `./gameserver u`

Update will check for an update. If there is an update it will download and apply it, restarting the server if already running. If there is no update LinuxGSM will take no action.

# Automatic update

## Update on start

You can update your server on start, by editing your game main script.

`updateonstart="on"`

This will cause the server to take longer to start but can be useful for servers that are kept offline most of the time such as match servers.

## Scheduled updates

You can set a cronjob to run the update function at any given time.

To edit your cronjobs, type: 

`crontab -e`

You can run a cronjob as the `gameserver user` or as `root`, this choice is down to personal preference. 
Remember to amend the examples to match your server.

Here is an example of a user based cronjob to check for an update once an hour. 

`0 * * * *  /home/username/gameserver update > /dev/null 2>&1`

Here is an example of a root based cronjob to check for an update once an hour. 
> Note the extra `su - username -c` this indicates which user to run the script as. 

`0 * * * *  su - username -c '/home/username/gameserver update' > /dev/null 2>&1`

It is not recommended you check for updates more than once per hour.

If you want to make your own cronjob crontab.guru is a great resource to generate cronjobs.
https://crontab.guru/

## Force Update

See [[force-update]]


# Validate

See [[validate]]

Sometimes, things can go wrong SteamCMD can mess up, you can have corrupt files or files fail to download properly.
So if your server isn't starting after an update, or if it's still at the same server version, run the validate command.

`./gameserver validate`  
`./gameserver v`

> Note: if you modified core server files, they will be restored to their original version.

# Updating your LinuxGSM script
LinuxGSM has the ability to self update functions. It is recommended that you regularly run this command to get the latest version of LinuxGSM.

# update-functions

`./gameserver update-functions`  
`./gameserver uf`