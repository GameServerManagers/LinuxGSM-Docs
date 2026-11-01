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
Requires LinuxGSM v26.5.0 or later. See [Updating LinuxGSM](../commands/update-lgsm.md) for existing installations.
{% endhint %}

Use `extraparams` to add command-line parameters without replacing the default `startparameters`. LinuxGSM automatically appends its value to the end of `startparameters`. An empty or unset `extraparams` adds nothing.

Set it in your [LinuxGSM config](linuxgsm-config.md): the instance config for one server, or `common.cfg` for all instances of the same installation. The usual config precedence applies: an `extraparams` value in the instance config replaces the value in `common.cfg`; they are not combined. Secret configs can also set `extraparams`.

For example, to add a LAN setting to a No More Room in Hell server:

```bash
# lgsm/config-lgsm/nmrihserver/nmrihserver.cfg
## Extra Parameters | https://docs.linuxgsm.com/configuration/start-parameters#extra-parameters
extraparams="+sv_lan 1"
```

| Config                    | Executable                                              |
| ------------------------- | ------------------------------------------------------- |
| `extraparams="+sv_lan 1"` | `./srcds_run -game nmrih ... -maxplayers 8 +sv_lan 1` |

This is the recommended way to add parameters. If you leave the default `startparameters` in use, you continue to receive changes to it when LinuxGSM is updated. Check the resulting command line with `./gameserver details`.

{% hint style="warning" %}
LinuxGSM also appends `extraparams` when you override `startparameters`. Do not include `${extraparams}` in your own `startparameters` line: this would add the parameters twice.
{% endhint %}

`extraparams` can only add parameters at the end. Unreal Engine `?Option=value` options must be part of the map URL: use a predefined setting where available, or edit the URL in a `startparameters` override. For Minecraft Java servers, use `javaram` for the memory limit or `preexecutable` for other JVM options, which must appear before `-jar`.

## Additional Parameters

`startparameters` defines the command-line parameters passed after the server executable. Setting it in your config replaces the entire default line.

Use [Predefined Parameters](#predefined-parameters) to change an existing setting where possible. If you need to remove a parameter, change one without a predefined setting, or insert an option at a specific position, copy `startparameters` from `_default.cfg` into your instance config and edit it.

{% hint style="warning" %}
An overridden `startparameters` no longer receives changes to the default line when LinuxGSM is updated. Compare it with `_default.cfg` after updates. To add parameters at the end without replacing the defaults, use [Extra Parameters](#extra-parameters).
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
