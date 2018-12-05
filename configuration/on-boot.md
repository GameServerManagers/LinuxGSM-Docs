# Running on-boot

## Running on Boot

Multiple options are available to run your servers on boot. Pick the one that fits your configuration the best.

## Crontab

The crontab will allow you to create \[\[cronjobs\]\] that allow you to run a command on a set time or on boot. The below examples uses `@reboot` that will run a command on boot.

```bash
    @reboot '/home/username/gameserver monitor' > /dev/null 2>&1
```

> note: Most admins will also have a timed monitor cronjob configured. If you do not want to have extra cronjobs the timed monitor will also start a server but with a timed delay.

### Using `monitor` command \(recommended\)

After a reboot, any game server that has a "started" status will be started on boot. Servers that were manually stopped will remain stopped.

```bash
crontab -e
@reboot su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
```

To learn more, see [cronjobs](https://github.com/GameServerManagers/LinuxGSM/wiki/Cronjobs) and [automated monitoring](https://github.com/dgibbs64/linuxgsm/wiki/Monitor#automated-monitoring).

### Using `start` command

Start a game server unconditionally, even if you manually stopped a server.

```bash
crontab -e
@reboot su - username -c '/home/username/gameserver start' > /dev/null 2>&1
```

To learn more, see [Start-Stop-Restart](https://github.com/GameServerManagers/LinuxGSM/wiki/Start-Stop-Restart)

### Using `rc.local`

rc.local is another method to run scripts on boot. Any commands added to the rc.local file will run on boot.

```bash
nano /etc/rc.local
su - username -c '/home/username/gameserver start'
```

