# send

LinuxGSM comes with a game server `send` command.

## Commands

Standard: `./gameserver send your_command_here`

Send will send a command to the gameserver, as if it were entered into the console of the gameserver.

### Scheduled Commands

A [cronjob](../configuration/cronjobs.md) can be set to run `send` at any given time.

To edit cronjobs,. type:

`crontab -e`

A cronjob can be run as the `gameserver user` or as `root`, this choice is down to personal preference. Remember to amend the examples to match a specific game server.

Here is an example of a user based cronjob to send a message to a server every hour.

```text
0 * * * * /home/username/gameserver send "Test Message" > /dev/null 2>&1
```

Here is an example of a root based cronjob to send a message once every hour.

{% hint style="info" %}
The extra `su - username -c` indicates which user to run the script as.
{% endhint %}

```text
0 * * * * su - username -c '/home/username/gameserver send "Test Message"' > /dev/null 2>&1
```

[crontab.guru](https://crontab.guru/) is a great resource to generate cronjobs.

