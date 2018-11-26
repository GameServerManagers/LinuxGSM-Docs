# monitor

The `monitor` command checks that a server is up and running and restarts the server should it not be responding after several unsuccessful queries

Monitor uses different checks to ensure the server is running, first checking the server proccess is running then using gamedig or gsquery to confirm the game server is responding.

> Note: If the server was stopped manually, then `monitor` will not function until the server is manually started again.

## Commands

Standard: `./gameserver monitor`

Short: `./gameserver m`

## Automated Monitoring

Monitor is designed to be used automatically with cronjobs to allow a game server to be frequently checked.

As a reminder, you can edit your cronjobs, typing :

```text
crontab -e
```

> Note: Replace the username and gameserver according to your requirements

Here is an example of a user based cronjob to monitor your server every 5 minutes :

```text
*/5 * * * *  /home/username/gameserver monitor > /dev/null 2>&1
```

Here is an example of a root based cronjob to monitor your server every 5 minutes :

```text
*/5 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
```

To learn more about automation, see \[\[Cronjobs\]\]

## Alert Notifications

To be notified when a server fails alert notifications can be setup , see \[\[Alerts\]\].

## Boot startup

You can use monitor to run your server at boot under certain conditions. See \[\[On-Boot\]\]

## How does monitor work?

Monitor will first check if the server process \(or tmux session\) is running. If it is, it will then attempt to query the server using \[\[gamedig\]\] or \[\[gsquery.py\]\]. Should this fail to query it will attempt to query every 15 seconds over 60 second period. Should this fail the server will be rebooted.

The monitor will wait for 60 seconds as it is common for servers to stop responding to queries during a map change. This wait prevents monitor from rebooting a server that does not require it.

> Note: During server start, map change, workshop downloads, the server is unable to answer queries.

## Lockfile

LinuxGSM creates a lock file when `./gameserver start` is run. Monitor uses this lock file to confirm if an admin wants the server to be started. Should the lock file not be present monitor will not take any action. This is to prevent the scenario of an admin stopping the server only to have monitor start it up again a few minutes later.

