# Email

![](http://i.imgur.com/kP4Doap.png)

## Sending emails

LinuxGSM will send an email using the `mail` command.

Postfix or equivalent must be setup and correctly configured before sending emails. Failure to correctly configure Postfix and a domain for your server will mean that the email alert may be flagged as spam or not arrive at all. Configuring postfix is not covered here, but there are many tutorials online to help.

## Enable Email alerts

To enable email alerts you will need to add an email address to the [LinuxGSM config](../configuration/linuxgsm-config.md).

```bash
# Email Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Email
emailalert="off"
email="email@example.com"
emailfrom=""
```

## Send Test Alert

Finally test that everything correctly works by sending a test alert.

```text
./gameserver test-alert
```

