# Mailgun

[![Mailgun logo](../.gitbook/assets/mailgun_logo.png)](https://www.mailgun.com/)

[Mailgun](https://www.mailgun.com) is an email service that allows LinuxGSM to send emails via an API, bypassing the need to use postfix. This method of sending email notifications is generaly more reliable.

An option to setup Mailgun as an email relay in postfix is also available. The free package allows sending 10,000 emails per month.

```text
# Mailgun Email Alerts | https://docs.linuxgsm.com/alerts/mailgun
mailgunalert="off"
mailguntoken="accesstoken"
mailgundomain="example.com"
mailgunemailfrom="alert@example.com"
mailgunemail="email@myemail.com"
```

