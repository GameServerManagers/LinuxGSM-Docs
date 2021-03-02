# monitor

`monitor` checks the game server to ensure the server functioning. First checking the game server process is running then querying the game server to check the game server is responding. monitor is designed to be an automated command that frequently checks the game server, rebooting and alerting if required.

## Commands

Standard: `./gameserver monitor`

Short: `./gameserver m`

## How does monitor work?

Monitor first checks that the server process or [tmux](../requirements/tmux.md) session is running. If it is, it will then attempt to query the server using [gamedig](../requirements/gamedig.md) or [gsquery.py](monitor.md). Should this fail to query it will attempt to query every 15 seconds over 60 second period. Should this fail the server will be rebooted and an alert sent out.

During server start, map change, workshop downloads, the server is unable to answer queries.The monitor will wait for 60 seconds as it is common for servers to stop responding to queries during a map change. This wait prevents monitor from rebooting a server that does not require it.

## Automated Monitoring

Monitor is designed to be and automated task, using [cronjobs](../configuration/cronjobs.md) to allow a game server to be frequently checked.

As a reminder, you can edit your cronjobs, typing :

```text
crontab -e
```

### Monitor Cronjob

Use these cron examples to setup automated monitoring.

{% hint style="info" %}
Replace the username and gameserver according to your requirements.
{% endhint %}

* A _user_ based cronjob to monitor your server every 5 minutes .

```text
*/5 * * * *  /home/username/gameserver monitor > /dev/null 2>&1
```

* A _root user_ based cronjob to monitor your server every 5 minutes .

```text
*/5 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
```

To learn more about automation, see [Cronjobs](../configuration/cronjobs.md).

## Alert Notifications

To be notified when a server fails alert notifications can be setup , see [alerts](../alerts/).

## Query Delay

Game Servers do not respond to queries while the server is booting. Query delay prevents monitor from giving a false positive should it query while the server is booting. A timed delay prevents monitor from using query at all during a set time \(normally either 1 or 5 minutes\) after start, giving the server time to boot and become ready to accept queries. Query delay timer can be adjusted using the `querydelay` setting.

```text
## Monitor | https://docs.linuxgsm.com/commands/monitor
# Query delay time
querydelay="1"
```

## Monitor Activation

Starting and stopping the game server activates and deactivates `monitor`. This prevents the server being manually stopped only to be started again by `monitor`.

