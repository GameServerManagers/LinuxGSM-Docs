# Start Parameters

Servers commonly require _start parameters_, these are command-line options that are set with the servers executable when you start the server. Parameters being used by the game server can be found in `./gameserver details`. To alter them, you will need to edit [LinuxGSM config files](linuxgsm-config.md).

LinuxGSM prefers to use config files over parameters as much as possible. However sometimes this is not possible, win which case only parameters or a mixture of both config and parameters will be used. LinuxGSM also attempts to keep the same method between game servers of the same engine to allow consistency between game servers.

##  Predefined Start Parameters

LinuxGSM often comes with predefined parameters that can be edited. This makes adjusting common settings a easier and allow them to be displayed in `./gameserver details`.

```text
## Server Start Settings
defaultmap="map_name"
gamemode="game_mode"
maxplayers="42"
port="27015"
sourcetvport="27020"
clientport="27005"
```

## Additional Parameters

Additional command-line parameters can be added to the `parms` variable. Anything added will be appended to the server executable binary.

### Basic Example

| Parms variable | Executable |
| :--- | :--- |
| `parms="-game nmrih"` | `./srcds_run -game nmrih` |

###  Full Example

```text
## Server Start Parameters | https://github.com/GameServerManagers/LinuxGSM/wiki/Start-Parameters
fn_parms(){
parms="-game nmrih -strictportbind -ip 91.121.72.41 -port 27015 +clientport 27017 +tv_port 27016 +map nmo_broadway +servercfgfile nmrih-server-1.cfg -maxplayers 8"
}
```

## Parameters reference

* 7 Days to Die: [http://7daystodie.gamepedia.com/Server](http://7daystodie.gamepedia.com/Server)
* Gold Source Servers: [https://developer.valvesoftware.com/wiki/Command\_Line\_Options\#Goldsource\_Games](https://developer.valvesoftware.com/wiki/Command_Line_Options#Goldsource_Games)
* Source Dedicated Servers: [https://developer.valvesoftware.com/wiki/Command\_Line\_Options\#Source\_Dedicated\_Server](https://developer.valvesoftware.com/wiki/Command_Line_Options#Source_Dedicated_Server)
* NS2 Server: [http://wiki.unknownworlds.com/ns2/Dedicated\_Server](http://wiki.unknownworlds.com/ns2/Dedicated_Server)
* Rust: [https://developer.valvesoftware.com/wiki/Rust\_Dedicated\_Server](https://developer.valvesoftware.com/wiki/Rust_Dedicated_Server)
* Serious Sam 3: [https://raw.githubusercontent.com/GameServerManagers/Game-Server-Configs/master/SeriousSam3BFE/help/DedicatedServer\_Readme.txt](https://raw.githubusercontent.com/GameServerManagers/Game-Server-Configs/master/SeriousSam3BFE/help/DedicatedServer_Readme.txt)
* Squad: [http://squad.gamepedia.com/Server\_Configuration\#Command\_Line](http://squad.gamepedia.com/Server_Configuration#Command_Line)
* Killing Floor 2: [https://wiki.tripwireinteractive.com/index.php?title=Dedicated\_Server\_\(Killing\_Floor\_2\)\#Advanced\_Configuration](https://wiki.tripwireinteractive.com/index.php?title=Dedicated_Server_%28Killing_Floor_2%29#Advanced_Configuration)

