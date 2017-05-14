# Running on Boot

Multiple options are available to run your servers on boot. Pick the one that fits your configuration the best.

## Using `monitor` command (recommended)

After a reboot, a game server that was on a "started" status will be started back. Servers that were manually stopped will remain stopped.
- Pro: Won't start servers that were manually shut down
- Con: Takes a few minutes to start (the time you set for your monitor)

Example (as root; replace "username" and "gameserver" accordingly):
````bash
crontab -e
*/3 * * * * su - username -c '/home/username/gameserver start' > /dev/null 2>&1
````

To learn more, see [cronjobs](https://github.com/GameServerManagers/LinuxGSM/wiki/Cronjobs) and [automated monitoring](https://github.com/dgibbs64/linuxgsm/wiki/Monitor#automated-monitoring).

## Using `start` command

Start a game server unconditionally.
- Pro: No delay to start the server after a reboot
- Con: Might start servers that you stopped and wouldn't want back online

Example (as root; replace "username" and "gameserver" accordingly):
````bash
crontab -e
@reboot su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
````

To learn more, see [Start-Stop-Restart](https://github.com/GameServerManagers/LinuxGSM/wiki/Start-Stop-Restart)

## Using `rc.local`

Add a command in to the rc.local file. 

- Cons: You might forget it's here, away from other cronjobs; it might start servers that you stopped and wouldn't want back online

Example (as root; replace "username" and "gameserver" accordingly):
````bash
nano /etc/rc.local
su - username -c '/home/username/gameserver start'
````