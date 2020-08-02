# Start Parameters

Many game servers require _start parameters_, these are command-line options that are set with the servers executable when the server starts. 

Using [game server configs](game-server-config.md) over parameters is prefered, however, sometimes this is not an option. When this is the case only parameters or a mixture of game server config and parameters will be used.

Parameters being used by the game server can be found in `./gameserver details`. To alter them, you will need to edit [LinuxGSM config files](linuxgsm-config.md).

## Predefined Parameters

LinuxGSM often uses predefined parameters that can be edited. This makes adjusting common settings easier and allows them to be displayed in `./gameserver details`.

```text
## Predefined Parameters | https://docs.linuxgsm.com/configuration/start-parameters
defaultmap="map_name"
gamemode="game_mode"
maxplayers="42"
port="27015"
sourcetvport="27020"
clientport="27005"
```

## Additional Parameters

Additional command-line parameters can be added to the `parms` setting. 

Anything added will be appended to the server executable binary.

### Basic Example

| Parms variable | Executable |
| :--- | :--- |
| `parms="-game nmrih"` | `./srcds_run -game nmrih` |

### Full Example

```text
## Server Parameters | https://docs.linuxgsm.com/configuration/start-parameters#additional-parameters
fn_parms(){
parms="-game nmrih -strictportbind -ip 91.121.72.41 -port 27015 +clientport 27017 +tv_port 27016 +map nmo_broadway +servercfgfile nmrih-server-1.cfg -maxplayers 8"
}
```

## Parameters reference

* 7 Days to Die: [http://7daystodie.gamepedia.com/Server](http://7daystodie.gamepedia.com/Server)
* Gold Source Servers: [https://developer.valvesoftware.com/wiki/Command\_Line\_Options\#Goldsource\_Games](https://developer.valvesoftware.com/wiki/Command_Line_Options#Goldsource_Games)
* Source Dedicated Servers: [https://developer.valvesoftware.com/wiki/Command\_Line\_Options\#Source\_Dedicated\_Server](https://developer.valvesoftware.com/wiki/Command_Line_Options#Source_Dedicated_Server)
* Memories Of Mars: [https://memoriesofmars.gamepedia.com/Dedicated\_Servers\#Overriding\_with\_Commandline\_Arguments](https://memoriesofmars.gamepedia.com/Dedicated_Servers#Overriding_with_Commandline_Arguments)
* NS2 Server: [http://wiki.unknownworlds.com/ns2/Dedicated\_Server](http://wiki.unknownworlds.com/ns2/Dedicated_Server)
* Rust: [https://developer.valvesoftware.com/wiki/Rust\_Dedicated\_Server](https://developer.valvesoftware.com/wiki/Rust_Dedicated_Server)
* Serious Sam 3: [https://raw.githubusercontent.com/GameServerManagers/Game-Server-Configs/master/SeriousSam3BFE/help/DedicatedServer\_Readme.txt](https://raw.githubusercontent.com/GameServerManagers/Game-Server-Configs/master/SeriousSam3BFE/help/DedicatedServer_Readme.txt)
* Squad: [http://squad.gamepedia.com/Server\_Configuration\#Command\_Line](http://squad.gamepedia.com/Server_Configuration#Command_Line)
* Killing Floor 2: [https://wiki.tripwireinteractive.com/index.php?title=Dedicated\_Server\_\(Killing\_Floor\_2\)\#Advanced\_Configuration](https://wiki.tripwireinteractive.com/index.php?title=Dedicated_Server_%28Killing_Floor_2%29#Advanced_Configuration)

