# LinuxGSM Config

{% hint style="info" %}
_LinuxGSM Configs_ and [_Game Server Configs_](game-server-config.md) are different. One is the config for LinuxGSM itself and the other is for the game server instance.
{% endhint %}

LinuxGSM configuration is managed using multiple config files loaded in a set order. It is important to understand how these config files work to make sure settings are placed in the correct config files.

## Config Files Location

Relative to your installation directory, config files are located in:

```text
lgsm/config-lgsm/gameserver
```

## Configuration Mechanism

The LinuxGSM config mechanism is designed to allow the users to benefit from new features, maintain default settings, better manage multiple instances and allow LinuxGSM to update the config if required.

### Configuration files

{% hint style="info" %}
An understanding of how LinuxGSM handles [multiple game server](../features/multiple-game-servers.md) instances helps.
{% endhint %}

#### \_default.cfg

`_default.cfg` is the template config: The file is a base of all available default settings. It can not be edited and is updated by LinuxGSM when using `./gameserver update-lgsm`. This config is loaded first.

{% hint style="warning" %}
Do not edit \_default.cfg any changes to this file will be overwritten
{% endhint %}

#### common.cfg

`common.cfg` is used for common settings that apply to all game server instances of the same installation. This saves having to apply the same settings multiple times.

#### instance.cfg

`instance.cfg` is the configuration file used for each individual game server instance. Settings here will only apply to this specific game server instance. This config file takes the same name as the game server script `./gameserver`. For example if `./csgoserver` is used the _instance.cfg_ will be called `csgoserver.cfg`. This config is last to be loaded.

### Config Load Priority

When LinuxGSM is loading the configs they will load in order. First taking settings from `_default.cfg` then `common.cfg` and finally `instance.cfg`. This means that any setting set in `instance.cfg` will override that setting in `common.cfg` which in turn will override the setting in `_default.cfg`.

{% code title="LinuxGSM config load order" %}
```text
_default.cfg -> common.cfg -> instance.cfg
```
{% endcode %}

## How to use

**Warning**: When changing a variable that affects start parameters, or any other variable that are used later in the configuration file, you should always make sure that you copied the variable or function that is using it. For example, if changing `maxplayers=""`, you need to copy over the `fn_parms(){}` entirely as well so that it can take effect. If unsure, do as advised in the "Simple configuration" method and copy the whole template to your configuration file and you will be just fine.

### Simple configuration

This fits most scenarios, where you have a simple installation with only one instance.

1\) Browse to the `config-lgsm` directory  
`cd lgsm/config-lgsm/`

2\) Use `ls` to view the content and find the name of your instance \(typically the name of your LinuxGSM server instance\)  
`ls`

3\) Copy the default config to your instance's config  
`cat _default.cfg >> instance.cfg`  
\(replace "instance.cfg" by your actual instance config name, for example "csgoserver.cfg" or "csgoserver-2.cfg"\)

Now you can edit your instance file that contains all of your LinuxGSM and start parameters configuration.

4\) \(Optional\) Remove any part of the config of your `instance.cfg` that you want defaulted to benefit from new default settings automatically added in `_default.cfg`.

### Multiple instances configuration

> This is only useful when running multiple instances of this install as per [Multiple Game Servers](../features/multiple-game-servers.md).

1\) Start by copying `_default.cfg` to `common.cfg`  
`cat _default.cfg >> common.cfg`

2\) \(Optional\) Remove any part of the config of your `common.cfg` that you want defaulted to benefit from new default settings automatically added in `_default.cfg`

3\) Then edit your multiple `instance.cfg` files manually, copying the parameters that you need to be customized. It's best to use two SSH windows to be more efficient. Usually, you will want to set individually the IP, ports, server name and map if applicable, and set the rest from `common.cfg` or from `_default.cfg`

4\) Then you can check that your servers work properly together, stop those you need to work on, and work on your [Game Server Config](game-server-config.md)

### Examples

Any setting listed in `instance.cfg` will override `common.cfg` which will override `_default.cfg`. And the other way around, any setting that is not listed in `instance.cfg` will take the value of the first parent config file where the value is set.

#### Example 1

Load `de_nuke` as default map on "csgoserver":

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
csgoserver.cfg: defaultmap="de_nuke"
```

#### Example 2

Load `cs_office` as default map on "csgoserver":

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: defaultmap="cs_office"
csgoserver.cfg: NOT SET
```

#### Example 3

Load `de_dust2` as default map on "instance":

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
instance.cfg: NOT SET
```

#### Example 4

Load `de_nuke` as default map on "myawesomeinstance" and `de_inferno` on "mynewserver":

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: defaultmap="de_inferno"
myawesomeinstance.cfg: defaultmap="de_nuke"
mynewserver.cfg: NOT SET
```

