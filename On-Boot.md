# Running on Boot
To run a server on boot, at least two ways are available.

## Using monitor (recommended)

After a reboot, a gameserver that was started (even crashed) will be started back.

Example (as root; replace "username" and "gameserver" accordingly):
````bash
crontab -e
*/3 * * * * su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
````

To learn more, see [cronjobs](https://github.com/GameServerManagers/LinuxGSM/wiki/Cronjobs) and [automated monitoring](https://github.com/dgibbs64/linuxgsm/wiki/Monitor#automated-monitoring).

## Using rc.local

Add a command in to the rc.local file. That works with most distro. 

Example (as root; replace "username" and "gameserver" accordingly):
````bash
nano /etc/rc.local
su - username -c '/home/username/gameserver start'
````