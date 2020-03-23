---
description: 'Sourcemod CS:GO Manual Install Guide and Known Problems'
---

# Installing Sourcemod on CS:GO Server

Sourcemod is a plugin for source games that can add functionality such as new voting systems, minigames, and server utilities. 

**Sourcemod Official Resources**

[Sourcemod Download Link](https://www.sourcemod.net/downloads.php?branch=stable%20)

[Metamod Download Link](http://www.sourcemm.net/downloads.php?branch=stable%20)

[Official Sourcemod Install Guide](https://wiki.alliedmods.net/Installing_SourceMod%20)



**Note: Linuxgsm includes a command that is able to install sourcemod automatically.**  

[LinuxGSM Mod Com](https://docs.linuxgsm.com/commands/mods)[mand](https://docs.linuxgsm.com/commands/mods) 



**CS:GO Sourcemod tips:** 

If the server keeps changing map to dust or mirage instead of the chosen map, disable the nextmap plugin 

If players are kicked shortly after joining, make sure sourcemod does not have any errors and is up to date 



**How to manually install sourcemod:** 

Unpack the sourcemod and metamod archives in the /home/user/serverfiles/csgo/ folder or unpack the archives locally and copy the files to the server with ftp. 

This will unpack files inside the /csgo/addons/ and /csgo/cfg/ folders, and should only require a server restart for sourcemod to work.



**Sourcemod Plugins:** 

Plugins can be downloaded from Alliedmodders website: 

[https://forums.alliedmods.net/forumdisplay.php?f=123](https://forums.alliedmods.net/forumdisplay.php?f=123) 

[https://forums.alliedmods.net/forumdisplay.php?f=153](https://forums.alliedmods.net/forumdisplay.php?f=153) 



Sourcemod plugins are located in /home/user/serverfiles/csgo/addons/sourcemod/plugins/ 

To disable plugins, move them to the disabled folder or delete the plugin.

Be sure to check plugin archives before unpacking for correct folder hierarchy, not every plugin creator organizes their archive the same.

