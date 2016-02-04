# Monitoring your server

The monitor function allows you to check if a server is up and running, and restart it if it's down after several unsuccessful queries.

`./gameserver monitor`


## Email Notifications

Email notifications allow you to recieve an email if the server is monitored down and restarted. That notification will include some of the logs to help you diagnose what caused the crash. Make sure that you installed mailx and postfix.

To enable them, edit your script accordingly : 

`emailnotification="on"`

`email="email@example.com"`



## Automated monitoring

To learn more about automation, see https://github.com/dgibbs64/linuxgsm/wiki/Automation

### Every "x" time cronjobs

The whole point of this monitor function is to automate it using cronjobs. LGSM team advise you to use root cronjobs.

`crontab -e`


**ATTENTION !** Replace the username and gameserver according to your case


Here is an example of a user based cronjob to monitor your server every 3 minutes : 

`*/3 * * * *  '/home/username/gameserver monitor' > /dev/null 2>&1`

Here is an example of a root based cronjob to monitor your server every 3 minutes : 

`*/3 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1`