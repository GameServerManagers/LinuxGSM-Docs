The monitor function allows you to check if a server is up and running, and restart it if it's down after several unsuccessful queries.

`./gameserver monitor`

Note: If the server was stopped manually, then `monitor` won't restart it.

# Automated monitoring

The whole point of this monitor function is to automate it using cronjobs.

As a reminder, you can edit your cronjobs, typing : 

`crontab -e`


> ATTENTION: Replace the username and gameserver according to your requirements


Here is an example of a user based cronjob to monitor your server every 5 minutes : 

`*/5 * * * *  /home/username/gameserver monitor > /dev/null 2>&1`

Here is an example of a root based cronjob to monitor your server every 5 minutes : 

`*/5 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1`

To learn more about automation, see [[Cronjobs]]

## Alert Notifications

If you wish to get informed after a server was monitored down, see [[Email]] and [[Pushbullet]].

## Boot startup

You can use monitor to run your server at boot under certain conditions. See [[On-Boot]]

# How does monitor work?

Monitor will first check if the server process (or tmux session) is running. If it is, it will then attempt to query the server using [[gsquery.py]]. Should this fail to query it will attempt to re query every 15 seconds over 60 second period. Should this fail the server will be rebooted. 

The monitor will wait for 60 seconds because it is common for servers to stop responding to query's during a map change. This wait prevents monitor from rebooting a server that does not require it. 

## Lockfile
LinuxGSM creates a lock file when `./gameserver start` is run. Monitor uses this lock file to confirm if an admin wants the server to be started. Should the lock file not be present monitor will not take any action. This is to prevent the scenario of an admin stopping the server only to have monitor start it up again a few minutes later. 

Note: During server start, map change, workshop downloads, the server is unable to answer queries.