LinuxGSM manages its configuration using multiple config files. It is important you understand how these config files work.

> Note: If you have use the "legacy" LGSM (installed prior to 16.06.17), it is a good idea to backup and update your LinuxGSM scripts manually to benefit from new features and prevent from bogus upon script updates.

> Note: For game server configuration, see [[Game Server Config]].

# Location
Relative to your installation directory, config files are located in:

`lgsm/config-lgsm/gameserver`

# Configuration mechanism
The current config files management is meant to allow the users to more easily benefit from new features, better manage multiple instances and allow the auto update of `./gameserver` script file (previously manual updating was required).

## Configuration files

### _default.cfg
* `_default.cfg` is your template: you cannot edit this one. It is meant to always be defaulted and is automatically updated; this allows the addition of new features and provides default settings to start with.  
**Do not edit this one!**  
### common.cfg
* `common.cfg` is used when running multiple instances of the same installation (see [[Multiple Game Servers]]). This configuration file is shared for all instances; it is very handy to change all recurring settings at once.

### instance.cfg
* `instance.cfg` is the main configuration file: each game server's (instance) configuration file. This file takes the same name as your game server script name (instance name), for example `csgoserver.cfg`.

## Priority
When LinuxGSM is loading the configs they will load in the above order. First taking settings from `_default.cfg` then `common.cfg` and finally `instance.cfg`. It means that any parameter set in `instance.cfg` will override that parameter in `common.cfg` which will override the parameter in `_default.cfg`.

You can mix and match settings to suit your needs, using _default.cfg as a baseline.

# How to use

## Simple configuration

This fits most scenarios, where you have a simple installation with only one instance.

1) Browse to the `config-lgsm` directory  
`cd lgsm/config-lgsm/`

2) Use `ls` to view the content and find the name of your instance (typically the name of your LinuxGSM server instance)  
`ls`

3) Copy the default config to your instance's config  
`cat _default.cfg >> instance.cfg`  
(replace "instance.cfg" by your actual instance config name, for example "csgoserver.cfg" or "csgoserver-2.cfg")

Now you can edit your instance file that contains all of your LinuxGSM and start parameters configuration.

4) (Optional) Remove any part of the config of your `instance.cfg` that you want defaulted to benefit from new default settings automatically added in `_default.cfg`.

## Multiple instances configuration

> This is only useful when running multiple instances of this install as per [[Multiple Game Servers]].

1) Start by copying `_default.cfg` to `common.cfg`  
`cat _default.cfg >> common.cfg`

2) (Optional) Remove any part of the config of your `common.cfg` that you want defaulted to benefit from new default settings automatically added in `_default.cfg`

3) Then edit your multiple `instance.cfg` files manually, copying the parameters that you need to be customized. It's best to use two SSH windows to be more efficient. Usually, you will want to set individually the IP, ports, server name and map if applicable, and set the rest from `common.cfg` or from `_default.cfg`

4) Then you can check that your servers work properly together, stop those you need to work on, and work on your [[Game Server Config]]
  

## Examples

Any setting listed in `instance.cfg` will override `common.cfg` which will override `_default.cfg`. And the other way around, any setting that is not listed in `instance.cfg` will take the value of the first parent config file where the value is set.

### Example 1
Load `de_nuke` as default map on "csgoserver":
    _default.cfg: defaultmap="de_dust2"
    common.cfg: NOT SET
    csgoserver.cfg: defaultmap="de_nuke"

### Example 2
Load `cs_office` as default map on "csgoserver":
```
_default.cfg: defaultmap="de_dust2"
common.cfg: defaultmap="cs_office"
csgoserver.cfg: NOT SET
```

### Example 3
Load `de_dust2` as default map on "instance":
```
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
instance.cfg: NOT SET
```

### Example 4
Load `de_nuke` as default map on "myawesomeinstance" and `de_inferno` on "mynewserver":
```
_default.cfg: defaultmap="de_dust2"
common.cfg: defaultmap="de_inferno"
nukeonly.cfg: defaultmap="de_nuke"
mynewserver.cfg: NOT SET
```