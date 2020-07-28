# Mailgun

[![Mailgun logo](../.gitbook/assets/mailgun_logo.png)](https://www.mailgun.com/)

[Mailgun](https://www.mailgun.com) is a paid-for email service that allows LinuxGSM to send emails via an API, bypassing the need to use postfix. This method of sending email notifications is generally more reliable.

An option to setup Mailgun as an email relay in postfix is also available. 

Mailgun's Flex Package allows 3 free months up to 5000 emails then turns into a pay-as-you-go plan afterwards.

```text
# Mailgun Email Alerts | https://docs.linuxgsm.com/alerts/mailgun
mailgunalert="off"
mailguntoken="accesstoken"
mailgundomain="example.com"
mailgunemailfrom="alert@example.com"
mailgunemail="email@myemail.com"
```

