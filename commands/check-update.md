# check-update

LinuxGSM comes with a game server `check-update` command. All [SteamCMD](../steamcmd/) games servers are supported, as well as some other servers such as Teamspeak, Minecraft, Mumble & Factorio.

## Commands

Standard: `./gameserver check-update`

Short: `./gameserver cu`

Unlike the [update](update.md) command `check-update` will check for any available updates and take no action if no update is available. If there is an update it will send an alert.

## Automatic check for update

### Scheduled check for updates

A [cronjob](../configuration/cronjobs.md) can be set to run `check-update` at any given time.

{% hint style="warning" %}
Ensure that an [alert](../alerts/) is configured so you are alerted to any updates
{% endhint %}

To edit cronjobs, type:

`crontab -e`

A cronjob can be run as the `gameserver user` or as `root`, this choice is down to personal preference. Remember to amend the examples to match a specific game server.

Here is an example of a user-based cronjob to check for an update once an hour.

```
0 * * * * /home/username/gameserver check-update > /dev/null 2>&1
```

Here is an example of a root-based cronjob to check for an update once an hour.

{% hint style="info" %}
The extra `su - username -c` indicates which user to run the script as.
{% endhint %}

```
0 * * * * su - username -c '/home/username/gameserver update' > /dev/null 2>&1
```

[crontab.guru](https://crontab.guru/) is a great resource to generate cronjobs.
