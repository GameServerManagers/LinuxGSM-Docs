# Killing Floor 2

## Ports

**Game Port** Default: 7777 UDP Handled by: `LinuxServer-KFEngine.ini` **Query Port** Default: 27015 UDP Handled automatically or handled by parameters. Formula for finding query port assigned automatically is 19238 + assigned game port. **Web Admin** Default: 8080 TCP Handled by: `KFWeb.ini` **Steam Port** Default: 20560 UDP Handled automatically. Formula for finding steam port is 12783 + assigned game port.

## Resources

[Killing Floor 2 Official Server Wiki](https://wiki.tripwireinteractive.com/index.php?title=Dedicated_Server_%28Killing_Floor_2%29)

## Workshop Map Warning!

There is a possible bug with KF2 dedicated servers using the steam workshop to host content that causes the server to constantly read/write and disk IO to be %100. This will severely increase hardware degradation. This was apparently fixed late 2019 but seems to have resurfaced with the recent Neon Nightmares 2020 update.

Disk IO can be monitored with the linux command:

iotop

References:

[https://forums.tripwireinteractive.com/index.php?threads/twi-you-destroyed-my-kf2-servers-ssd.2334936/](https://forums.tripwireinteractive.com/index.php?threads/twi-you-destroyed-my-kf2-servers-ssd.2334936/)

[https://forums.tripwireinteractive.com/index.php?threads/server-is-going-disk-drive-crazy.2333489/](https://forums.tripwireinteractive.com/index.php?threads/server-is-going-disk-drive-crazy.2333489/)





