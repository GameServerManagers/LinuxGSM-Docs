# check-update

LinuxGSM comes with an game server `check-update` command. All [SteamCMD](../steamcmd/) games servers are supported.

## Commands

Standard: `./gameserver check-update`

Short: `./gameserver cu`

Check-update will check for any available update, taking no action if no update is available. If there is an update it will send a alert if one is set up.

## Automatic check for avaliupdate 

### Scheduled check for updates updates

A [cronjob](../configuration/cronjobs.md) can be set to run `check-update` at any given time.

Currently a cronjob is only makes sense if a [Alert](../alerts/README.md) is set up.

To edit cronjobs, type:

`crontab -e`

A cronjob can be run as the `gameserver user` or as `root`, this choice is down to personal preference. Remember to amend the examples to match a specific game server.

Here is an example of a user based cronjob to check for an update once an hour.

```text
0 * * * * /home/username/gameserver check-update > /dev/null 2>&1
```

Here is an example of a root based cronjob to check for an check-update once an hour.

{% hint style="info" %}
The extra `su - username -c` indicates which user to run the script as.
{% endhint %}

```text
0 * * * * su - username -c '/home/username/gameserver update' > /dev/null 2>&1
```

[crontab.guru](https://crontab.guru/) is a great resource to generate cronjobs.

