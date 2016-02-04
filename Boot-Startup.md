# Running on Boot
To run a server on boot, two ways are available. We advise you to use the monitor function


## Using monitor

Using a monitor cronjob, after a reboot, any server that had a "started" status, even if crashed, will be started back. Manually stopped servers won't restart after a reboot.

To do so, use [monitor function as a cronjob](https://github.com/dgibbs64/linuxgsm/wiki/Monitor#automated-monitoring)


## Using rc.local

Add a command in to the rc.local file. That works with most distro. Obviously, replace "username" and "gameserver" accordingly.

    nano /etc/rc.local
    su - username -c '/home/username/gameserver start'