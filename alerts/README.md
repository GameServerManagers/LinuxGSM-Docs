# Alerts

LinuxGSM allows alerts to be received using various methods, should the game server require your attention.

## Alert Settings

Alert settings can be changed in [LinuxGSM config](../configuration/linuxgsm-config.md)

### More Info

More info allows you to get further info about an alert using hastebin.com. Many alerts only give basic info, unlike email. More info displays the same output as email in a link within a basic alert.

```text
# More info | https://docs.linuxgsm.com/alerts#more-info
postalert="off"
```

### Display IP

The IP address you want to be displayed in alerts.

By default, the LinuxGSM alert will display the external internet facing IP. Failing this will fall back to the server IP. If the IP is incorrect it can be manually set using `displayip=""`.

```text
# Display IP | https://docs.linuxgsm.com/alerts#display-ip
displayip=""
```

