# Running on Boot

## Using systemd

systemd is the default init system for most modern distros.

You need to create a service file in `/etc/systemd/system/`

Example `ts3server.service`

```text
[Unit]
Description=LinuxGSM Teamspeak3 Server
After=network-online.target
Wants=network-online.target

[Service]
Type=forking
User=ts3server
WorkingDirectory=/home/ts3server
ExecStart=/home/ts3server/ts3server start
ExecStop=/home/ts3server/ts3server stop
Restart=no
RemainAfterExit=yes   #Assume that the service is running after main process exits with code 0

[Install]
WantedBy=multi-user.target
```

Replace the user and paths to fit your setup.

You need to reload the systemd-daemon once to make it aware of the new service file by `systemctl daemon-reload`

Now you can do

```bash
systemctl start ts3server # Start the server
systemctl stop ts3server  # Stop the server
systemctl enable ts3server # Enable start on boot
systemctl disable ts3server # Disable start on boot
```

## Crontab

The crontab will allow you to create [cronjobs](cronjobs.md) that allow you to run a command on a set time or on boot. The below examples uses `@reboot` that will run a command on boot.

```bash
    @reboot '/home/username/gameserver monitor' > /dev/null 2>&1
```

> note: Most admins will also have a timed monitor cronjob configured. If you do not want to have extra cronjobs the timed monitor will also start a server but with a timed delay.

### Using `monitor` command

After a reboot, any game server that has a "started" status will be started on boot. Servers that were manually stopped will remain stopped.

```bash
crontab -e
@reboot su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
```

To learn more, see [cronjobs](cronjobs.md) and [automated monitoring](../commands/monitor.md#automated-monitoring).

### Using `start` command

Start a game server unconditionally, even if you manually stopped a server.

```bash
crontab -e
@reboot su - username -c '/home/username/gameserver start' > /dev/null 2>&1
```

To learn more, see [Start-Stop-Restart](../commands/start-stop-restart.md)

## `rc.local`

rc.local is another method to run scripts on boot. Any commands added to the rc.local file will run on boot.

```bash
nano /etc/rc.local
su - username -c '/home/username/gameserver start'
```

