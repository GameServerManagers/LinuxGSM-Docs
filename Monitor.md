# Monitoring your server

The monitor function allows you to check if a server is up and running, and restart it if it's down after several unsuccessful queries.

`./gameserver monitor`


## Email Notifications

To enable them, edit your script accordingly : 

`emailnotification="on"`

`email="email@example.com"`

Also make sure that you installed mailx and postfix.



## Automated monitoring

To learn more about automation, see https://github.com/dgibbs64/linuxgsm/wiki/Automation

### Every "x" time cronjobs

**Replace the username and gameserver according to your case**

Here is an example of a user based cronjob to monitor your server every 3 minutes : 

`*/3 * * * *  '/home/username/gameserver monitor' > /dev/null 2>&1`

Here is an example of a root based cronjob to monitor your server every 3 minutes : 

`*/3 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1`