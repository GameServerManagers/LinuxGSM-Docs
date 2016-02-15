## Email Notifications

Email notifications allow you to recieve an email if the server is monitored down and restarted. That notification will include some of the logs to help you diagnose what caused the crash. Make sure that you installed mailx and postfix.

To enable them, edit your script accordingly : 

`emailnotification="on"`

`email="email@example.com"`