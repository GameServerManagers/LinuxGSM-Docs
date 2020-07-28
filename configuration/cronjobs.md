# cronjobs

To automate LinuxGSM you can set scheduled tasks using cronjobs, to run any command at any given time.

Commonly used scheduled tasks are:

* Automatically check for updates [\(update command\)](../commands/update.md)
* Automatically check for server crash and restart if needed [\(monitor command\)](../commands/monitor.md)
* Automatically keep LinuxGSM up to date [\(update-lgsm command\)](../commands/update-lgsm.md)
* Automatically restart the server at a given time [\(restart command\)](../commands/start-stop-restart.md)
* Automatically update and restart the server [\(force-update command\)](../commands/force-update.md)

## Crontab

To access and edit your cronjobs use crontab.

```bash
crontab -e
```

## Cronjob as a user or root

It is possible to set up cronjobs as any user including root. The recommended way is to set up cronjobs using the game servers user account. However, If you run several game server installations on your server you may want to centrally manage cronjobs then using root. 

### User cronjob

```bash
* * * * * [/path/to/script] [command] > /dev/null 2>&1
```

### Root cronjob

```bash
* * * * * su - username -c '[/path/to/script] [command]' > /dev/null 2>&1
```

## **Cronjob Timing Examples**

### Every single minute

```bash
* * * * *
```

### Every 30 minutes

```bash
*/30 * * * *
```

### Every hour

```bash
0 * * * *
```

### Every two hours

```bash
0 */2 * * *
```

### Every two hours at 30 minutes past the hour 

```bash
30 */2 * * *
```

### Every day at 5:10 PM

```bash
10 17 * * *
```

### Every Wednesday at 1 AM

```bash
0 1 * * * 3
```

### Every Five Days at 1 AM

```bash
0 1 */5 * *
```

## Cronjob Generator

If you are not used to setting up cronjobs you can use [crontab.guru](https://crontab.guru) as a great reference to get started.

## LinuxGSM Cronjobs examples

{% hint style="info" %}
Replace username and gameserver with your own details.
{% endhint %}

### Daily cronjob

Here is an example of a user based cronjob for a daily restart at 5 am.

```bash
0 5 * * *  /home/username/gameserver restart > /dev/null 2>&1
```

Here is an example of a root based cronjob for a daily restart at 5 am.

```bash
0 5 * * *  su - username -c '/home/username/gameserver restart' > /dev/null 2>&1
```

### Every X Time cronjobs

Here is an example of a user based cronjob to monitor your server every 5 minutes.

```bash
*/5 * * * *  /home/username/gameserver monitor > /dev/null 2>&1
```

Here is an example of a root based cronjob to monitor your server every 5 minutes.

```bash
*/5 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
```

## Complete Example

Below is a recommended basic example and will do the following:

* Monitor your server every 5 minutes.
* Check for an update every 30 minutes, update and restart only if an update is detected.
* Restart and check for an update every day at 4:30 AM
* Update check and update LinuxGSM every Sunday at midnight.

```bash
*/5 * * * * /home/username/gameserver monitor > /dev/null 2>&1
*/30 * * * * /home/username/gameserver update > /dev/null 2>&1
30 4 * * *  /home/username/gameserver force-update > /dev/null 2>&1
0 0 * * 0 /home/username/gameserver update-lgsm > /dev/null 2>&1
```

