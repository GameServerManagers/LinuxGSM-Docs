# Email

A Linux server's own email solution can be used to receive alerts about LinuxGSM.

## Sending emails

LinuxGSM will send an email using the `mail` command.

Postfix or equivalent must be setup and correctly configured before sending emails. Failure to correctly configure Postfix and a domain for your server will mean the email alert may be flagged as spam or not arrive at all. Configuring postfix is not covered here, but there are many tutorials online to help.

If you only need to relay outbound alert emails through an external SMTP provider rather than run a full mail server, [nullmailer](https://www.nongnu.org/nullmailer/) is a lightweight alternative to Postfix. On Debian/Ubuntu, LinuxGSM will detect an existing nullmailer setup (`/etc/nullmailer`) and install `mailutils` alongside it instead of `postfix`, so an existing nullmailer relay won't be overwritten by LinuxGSM's dependency check.

### Free SMTP relay options

Sending mail directly from a home/VPS IP is likely to be flagged as spam. Relaying through a dedicated email provider improves deliverability, and several offer a free tier suitable for the low volume of alert emails LinuxGSM sends:

| Provider | Free tier | Notes |
|---|---|---|
| [SMTP2GO](https://www.smtp2go.com/) | 1,000 emails/month | Permanently free, plain SMTP credentials, no card required |
| [Brevo](https://www.brevo.com/) | 300 emails/day | Permanently free, plain SMTP credentials; adds branding to emails on the free tier |
| [MailerSend](https://www.mailersend.com/) | 3,000 emails/month | Permanently free, SMTP + API, no branding on free tier |
| [Mailgun](https://www.mailgun.com/) | 100 emails/day | Permanently free (no longer a time-limited trial); requires domain verification |

Any of these can be used as the smarthost for Postfix or nullmailer — see the provider's SMTP relay setup docs for the exact Postfix/nullmailer configuration.

{% hint style="info" %}
Cloudflare added SMTP-based [Email Service](https://developers.cloudflare.com/email-service/) sending in 2026, but it currently requires a paid Workers plan for outbound sending, so it isn't a free option unless you already pay for Workers.
{% endhint %}

## Enable Email alerts

To enable email alerts you will need to add an email address to the [LinuxGSM config](../configuration/linuxgsm-config.md).

```bash
# Email Alerts | https://docs.linuxgsm.com/alerts/email
emailalert="off"
email="email@example.com"
emailfrom=""
```
