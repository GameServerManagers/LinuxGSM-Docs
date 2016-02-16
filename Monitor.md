# Monitoring your server

The monitor function allows you to check if a server is up and running, and restart it if it's down after several unsuccessful queries.

`./gameserver monitor`


## Automated monitoring

The whole point of this monitor function is to automate it using cronjobs. LGSM team advise you to use root cronjobs.

As a reminder, you can edit your cronjobs, typing : 

`crontab -e`


**ATTENTION !** Replace the username and gameserver according to your case


Here is an example of a user based cronjob to monitor your server every 3 minutes : 

`*/3 * * * *  /home/username/gameserver monitor > /dev/null 2>&1`

Here is an example of a root based cronjob to monitor your server every 3 minutes : 

`*/3 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1`

***

To learn more about automation, see [[Automation]]

## Email notifications

If you wish to get informed after a server was monitored down, see [[Email-Notifications]].