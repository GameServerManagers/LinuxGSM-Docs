# Email

A linux servers own email solution can be used to recieve alerts about LinuxGSM.

## Sending emails

LinuxGSM will send an email using the `mail` command.

Postfix or equivalent must be setup and correctly configured before sending emails. Failure to correctly configure Postfix and a domain for your server will mean that the email alert may be flagged as spam or not arrive at all. Configuring postfix is not covered here, but there are many tutorials online to help.

{% hint style="success" %}
[Mailgun](mailgun.md) can be used as an email relay to reduce the changes of email alerts being block as spam.
{% endhint %}

## Enable Email alerts

To enable email alerts you will need to add an email address to the [LinuxGSM config](../configuration/linuxgsm-config.md).

```bash
# Email Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Email
emailalert="off"
email="email@example.com"
emailfrom=""
```

