# update

LinuxGSM comes with an game server `update` command. All [SteamCMD](../steamcmd/) games servers are supported, as well as some other servers such as Teamspeak, Minecraft, Mumble & Factorio.

## Commands

Standard: `./gameserver update`

Short: `./gameserver u`

Update will check for any available update, taking no action if no update is available. If there is an update it will apply the update, restarting the server if already running.

## Automatic update

### Update on start

It is possible to update a game server on start, by editing the LinuxGSM config.

`updateonstart="on"`

This will take longer for the game server to start but can be useful for servers that are kept offline most of the time.

### Scheduled updates

A [cronjob](../configuration/cronjobs.md) can be set to run `update` at any given time.

To edit cronjobs, type:

`crontab -e`

A cronjob can be run as the `gameserver user` or as `root`, this choice is down to personal preference. Remember to amend the examples to match a specific game server.

Here is an example of a user based cronjob to check for an update once an hour.

```text
0 * * * * /home/username/gameserver update > /dev/null 2>&1
```

Here is an example of a root based cronjob to check for an update once an hour.

{% hint style="info" %}
The extra `su - username -c` indicates which user to run the script as.
{% endhint %}

```text
0 * * * * su - username -c '/home/username/gameserver update' > /dev/null 2>&1
```

It is recommended to check for updates once per hour.

crontab.guru is a great resource to generate cronjobs. [https://crontab.guru/](https://crontab.guru/)

