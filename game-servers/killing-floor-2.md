# Killing Floor 2

![](../.gitbook/assets/kf2banner.jpg)

## Ports

* **Game Port** Default: 7777 UDP Handled by: `LinuxServer-KFEngine.ini`&#x20;
* **Query Port** Default: 27015 UDP Handled automatically or handled by parameters. The formula for finding query port assigned automatically is 19238 + assigned game port.&#x20;
* **Web Admin** Default: 8080 TCP Handled by: `KFWeb.ini`&#x20;
* **Steam Port** Default: 20560 UDP Handled automatically. The formula for finding the steam port is 12783 + Game Port.

## Resources

[Killing Floor 2 Official Server Wiki](https://wiki.tripwireinteractive.com/index.php?title=Dedicated\_Server\_%28Killing\_Floor\_2%29)

[Killing floor 2 Official Forums](https://forums.tripwireinteractive.com/index.php?categories/killing-floor-2.25/)

## Server Config Information

LinuxGSM installations contain `configSubDir=servername` in the command line by default, which creates a folder for config files named after the server. The default directory is `/home/user/serverfiles/KFGame/Config/kf2server` . Use these files to change server settings.

## Workshop Content

Killing Floor 2 supports [Steam Workshop](../steamcmd/workshop.md).&#x20;

Players on the Epic Store will not be able to download files hosted with the Steam Workshop.

For KF2 Server using LinuxGSM, workshop content is added in `LinuxServer-KFEngine.ini` under:

/home/user/serverfiles/KFGame/Config/kf2server

[Official Guide Here](https://wiki.killingfloor2.com/index.php?title=Dedicated\_Server\_\(Killing\_Floor\_2\)#Setting\_Up\_Steam\_Workshop\_For\_Servers)

While following the guide, remember `PCServer-KFEngine.ini` is instead `LinuxServer-KFEngine.ini`

[Killing Floor 2 has a known workshop problem.](killing-floor-2.md)





