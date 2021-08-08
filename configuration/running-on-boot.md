# Running on Boot

## Using systemd

systemd is the default init system for most modern distros.
You can either generate and place the files contents using the install-init function, which will do it all for you, or do it manually.

- ### Using the install-init command

    Run `./<gameserver> install-init`, this will create and place the contents in `/etc/systemd/system/short name-lgsm.service`.
    The content will be based on the manual service file.


- ### Manual service file

    You need to create a service file in `/etc/systemd/system/`

    Example `gameserver.service`

    ```text
    [Unit]
    Description=LinuxGSM Game Server
    After=network-online.target
    Wants=network-online.target

    [Service]
    Type=forking
    User=gameserver
    WorkingDirectory=/home/gameserver
    RemainAfterExit=yes # Assume that the service is running after main process exits with code 0
    ExecStart=/home/gameserver/gameserver start
    ExecStop=/home/gameserver/gameserver stop
    Restart=no

    [Install]
    WantedBy=multi-user.target
    ```

    Replace the user and paths to fit your setup.



You need to reload the systemd-daemon once to make it aware of the new service file by `systemctl daemon-reload`

Now you can do (as root)

```bash
systemctl start gameserver # Start the server
systemctl stop gameserver # Stop the server
systemctl enable gameserver # Enable start on boot
systemctl disable gameserver # Disable start on boot
```

## Crontab

The crontab will allow you to create [cronjobs](cronjobs.md) that allow you to run a command on a set time or on boot. The below example uses `@reboot` that will run a command on boot.

```bash
    @reboot '/home/username/gameserver monitor' > /dev/null 2>&1
```

{% hint style="info" %}
Most admins will also have a timed monitor cronjob configured. If you do not want to have extra cronjobs the timed monitor will also start a server but with a timed delay.
{% endhint %}

### Using `monitor` command

After a reboot, any game server that has a "started" status will be started on boot. Servers that were manually stopped will remain stopped.

```bash
crontab -e
@reboot su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
```

To learn more, see [cronjobs](cronjobs.md) and [automated monitoring](../commands/monitor.md#automated-monitoring).

### Using `start` command

Start a game server unconditionally, even if you manually stop a server.

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

