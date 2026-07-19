# Email

A Linux server's own email solution can be used to receive alerts about LinuxGSM.

## Sending emails

LinuxGSM will send an email using the `mail` command.

Postfix or equivalent must be setup and correctly configured before sending emails. Failure to correctly configure Postfix and a domain for your server will mean the email alert may be flagged as spam or not arrive at all. Configuring postfix is not covered here, but there are many tutorials online to help.

If you only need to relay outbound alert emails through an external SMTP provider rather than run a full mail server, [nullmailer](https://www.nongnu.org/nullmailer/) is a lightweight alternative to Postfix. On Debian/Ubuntu, LinuxGSM will detect an existing nullmailer setup (`/etc/nullmailer`) and install `mailutils` alongside it instead of `postfix`, so an existing nullmailer relay won't be overwritten by LinuxGSM's dependency check.

{% hint style="success" %}
[Mailgun](broken-reference) is a paid service with 3 month free trial that can be used as an email relay to reduce the chances of email alerts being blocked as spam.
{% endhint %}

## Enable Email alerts

To enable email alerts you will need to add an email address to the [LinuxGSM config](../configuration/linuxgsm-config.md).

```bash
# Email Alerts | https://docs.linuxgsm.com/alerts/email
emailalert="off"
email="email@example.com"
emailfrom=""
```
