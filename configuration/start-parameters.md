# Start Parameters

Many game servers require _start parameters_, these are command-line options that are set with the servers executable when the server starts.&#x20;

Using [game server configs](game-server-config.md) over parameters is prefered, however, sometimes this is not an option. When this is the case only parameters or a mixture of game server config and parameters will be used.

Parameters being used by the game server can be found in `./gameserver details`. To alter them, you will need to edit [LinuxGSM config files](linuxgsm-config.md).

## Predefined Parameters

LinuxGSM often uses predefined parameters that can be edited. This makes adjusting common settings easier and allows them to be displayed in `./gameserver details`.

```
## Predefined Parameters | https://docs.linuxgsm.com/configuration/start-parameters
defaultmap="map_name"
gamemode="game_mode"
maxplayers="42"
port="27015"
sourcetvport="27020"
clientport="27005"
```

## Additional Parameters

Additional command-line parameters can be added to the `startparameters` setting.&#x20;

Anything added will be appended to the server executable binary.

### Basic Example

| Parms variable                  | Executable                |
| ------------------------------- | ------------------------- |
| `startparameters="-game nmrih"` | `./srcds_run -game nmrih` |

### Full Example

```
## Server Parameters | https://docs.linuxgsm.com/configuration/start-parameters#additional-parameters
startparameters="-game nmrih -strictportbind -ip 91.121.72.41 -port 27015 +clientport 27017 +tv_port 27016 +map nmo_broadway +servercfgfile nmrih-server-1.cfg -maxplayers 8"
```

## Parameters reference

* 7 Days to Die
* Gold Source Servers
* [Source Dedicated Servers](https://developer.valvesoftware.com/wiki/Command\_Line\_Options#Source\_Dedicated\_Server)
* [Memories Of Mars](https://memoriesofmars.gamepedia.com/Dedicated\_Servers#Overriding\_with\_Commandline\_Arguments)
* [Natural Selection 2](http://wiki.unknownworlds.com/ns2/Dedicated\_Server)
* [Rust](https://developer.valvesoftware.com/wiki/Rust\_Dedicated\_Server)
* [Squad](http://squad.gamepedia.com/Server\_Configuration#Command\_Line)
* [Killing Floor 2](https://wiki.tripwireinteractive.com/index.php?title=Dedicated\_Server\_\(Killing\_Floor\_2\)#Advanced\_Configuration)
