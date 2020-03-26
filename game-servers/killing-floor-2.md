# Killing Floor 2

## Ports

**Game Port** Default: 7777 UDP Handled by: `LinuxServer-KFEngine.ini` **Query Port** Default: 27015 UDP Handled automatically or handled by parameters. Formula for finding query port assigned automatically is 19238 + assigned game port. **Web Admin** Default: 8080 TCP Handled by: `KFWeb.ini` **Steam Port** Default: 20560 UDP Handled automatically. Formula for finding steam port is 12783 + assigned game port.

## Resources

[Killing Floor 2 Official Server Wiki](https://wiki.tripwireinteractive.com/index.php?title=Dedicated_Server_%28Killing_Floor_2%29)

[Killing floor 2 Official Forums](https://forums.tripwireinteractive.com/index.php?categories/killing-floor-2.25/)

## Server Config Information

Default linuxgsm installs have configSubDir=servername set in the command line which will set your priority config files to be in /home/user/serverfiles/KFGame/Config/kf2server directory, use these files to change settings on your server.

## Workshop Content Information

KF2 servers as of March 2020 will check workshop files at server start AND when map changes occur.

There is a possible problem with KF2 dedicated servers using the steam workshop to host content that causes the server disk usage to constantly read/write at %100. This will severely decrease hardware lifetime. 

To avoid this problem I suggest keeping the amount of workshop content as low as you can or changing files to fastDL. The only problem with FastDL is that Tripwire no longer supports it and files are not compressed, which increases download times. However, FastDL does not have a disk usage issue.

Disk IO can be monitored with the linux command:

iotop

References:

[TWI you destroyed my SSD forum post](https://forums.tripwireinteractive.com/index.php?threads/twi-you-destroyed-my-kf2-servers-ssd.2334936/)

[Server is going disk drive crazy forum post](https://forums.tripwireinteractive.com/index.php?threads/server-is-going-disk-drive-crazy.2333489/)

[Workshop map disk thrashing forum post](https://forums.tripwireinteractive.com/index.php?threads/workshop-map-disk-thrashing-is-back.2335275/)









