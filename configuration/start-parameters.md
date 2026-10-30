# Start Parameters



{% hint style="info" %}
Also known as Command-Line Parameters, Command line arguments, or Launch Parameters.
{% endhint %}

Many game servers require _start parameters_, these are command-line options that are set with the server executable when the server starts.&#x20;

Using [game server configs](game-server-config.md) over parameters is preferred, however, sometimes this is not an option. When this is the case only parameters or a mixture of game server config and parameters will be used.

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

## Extra Parameters

{% hint style="info" %}
Available from LinuxGSM v26.5.0.
{% endhint %}

To add your own parameters and keep the defaults, set `extraparams` in your [LinuxGSM config](linuxgsm-config.md) (usually the instance config). LinuxGSM adds them to the end of the start parameters.

```
## Extra Parameters | https://docs.linuxgsm.com/configuration/start-parameters#extra-parameters
extraparams="+sv_lan 1 +sv_pure 1"
```

| Config                          | Executable                                                      |
| ------------------------------- | --------------------------------------------------------------- |
| `extraparams="+sv_lan 1"`       | `./srcds_run -game nmrih ... -maxplayers 8 +sv_lan 1`           |

This is the recommended way to add parameters. The default `startparameters` stays untouched, so you keep getting changes to it when LinuxGSM is updated. `extraparams` is also added if you have overridden `startparameters`.

Check the result with `./gameserver details`.

{% hint style="warning" %}
`extraparams` is only added at the end of the command line. Options that have to be part of another parameter, such as Unreal Engine `?Option=value` map options, still need `startparameters`. For Minecraft servers, Java options belong in `javaram` or `preexecutable`, not `extraparams`.
{% endhint %}

## Additional Parameters

`startparameters` holds the full set of command-line parameters that are appended to the server executable binary.

Setting `startparameters` in your config replaces the default completely. It is not added to it. Only do this when you need to change or remove a default parameter. Copy the line from `_default.cfg` and edit it.

{% hint style="warning" %}
An overridden `startparameters` no longer receives changes to the defaults when LinuxGSM is updated. Compare it with `_default.cfg` after updating. To only add parameters, use [Extra Parameters](#extra-parameters) instead.
{% endhint %}

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
