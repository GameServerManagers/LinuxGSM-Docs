# Alerts

LinuxGSM allows alerts to be received using various methods, should the game server require your attention.

## Alert Settings

Alert settings can be changed in [LinuxGSM config](../configuration/linuxgsm-config.md)

### More Info

More info allows you to get further info about an alert using hastebin.com. Many alerts only give basic info, unlike email. More info displays the same output as email in a link within a basic alert.

```
# More info | https://docs.linuxgsm.com/alerts#more-info
postalert="off"
```

###

### Display IP

The IP address you want to be displayed in alerts.

By default, the LinuxGSM alert will display the external internet facing IP. Failing this will fall back to the server IP. If the IP is incorrect it can be manually set using `displayip=""`.

```
# Display IP | https://docs.linuxgsm.com/alerts#display-ip
displayip=""
```

### Alert Cooldown

The minutes to wait between repeated monitor alerts.

When a server keeps crashing or fails to start, [monitor](../commands/monitor.md) runs on every cron tick and sends an alert each time. With a cooldown set, only the first monitor alert is sent in each window. The rest are skipped and noted in the LinuxGSM log. Monitor still restarts the server on every run.

The cooldown applies to the "not running" and "unable to query" alerts. Started, stopped, update, backup and test alerts are always sent.

By default the cooldown is `0`, which sends every alert.

```
# Minutes to wait between repeated monitor alerts, 0 sends every alert
alertcooldown="0"
```

For example, `alertcooldown="60"` sends at most one monitor alert an hour for a server that keeps failing.
