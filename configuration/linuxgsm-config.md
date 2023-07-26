# LinuxGSM Config

{% hint style="info" %}
_LinuxGSM Configs_ and [_Game Server Configs_](game-server-config.md) are different. One is the config for LinuxGSM itself and the other is for the game server instance.
{% endhint %}

The configuration of LinuxGSM is handled through several config files, which are loaded in a specific order. Understanding this process is crucial to ensure that settings are appropriately placed within the correct config files.

## Config Files Location

Relative to your installation directory, config files are located in:

```
lgsm/config-lgsm/gameserver
```

## Configuration Mechanism

The LinuxGSM configuration mechanism is intentionally designed to provide users with several advantages. These include the ability to access new features, retain default settings, effectively handle multiple instances, and allow LinuxGSM to update the configuration when necessary.

### Configuration files

{% hint style="info" %}
An understanding of how LinuxGSM handles [multiple game server](../features/multiple-game-servers.md) instances helps.
{% endhint %}

#### \_default.cfg

`_default.cfg` is the template config, this file is a base of all available default settings. It can not be edited and is updated by LinuxGSM when using `./gameserver update-lgsm`. This config is loaded first.

{% hint style="warning" %}
Do not edit \_default.cfg any changes to this file will be overwritten.
{% endhint %}

#### common.cfg

`common.cfg` is used for common settings that apply to all game server instances of the same installation. This saves having to apply the same settings multiple times.

#### instance.cfg

`instance.cfg` is the configuration file used for each individual game server instance. Settings here will only apply to this specific game server instance. This config file takes the same name as the game server instance name `./gameserver`. For example, if `./csgoserver` is used the _instance.cfg_ will be called `csgoserver.cfg`. This config is last to be loaded.

### Secret Configs

{% hint style="danger" %}
Secret configs are not encrypted, but a place to store sensitive info away from other configs.
{% endhint %}

Secret configs serve as a designated space for storing sensitive information, such as steam login details, separately from the main config files. This separation allows server administrators to back up their configurations while excluding sensitive data, enhancing security and privacy. It proves especially valuable for administrators who wish to create a version-controlled skeleton configuration using git that might eventually become publicly accessible.

It's essential to understand that the secret config is not encrypted or inherently more secure than other config files. However, it provides a convenient way to keep sensitive information isolated from the rest of the configurations.

To distinguish secret configs from others, their names are typically prefixed with the word "secrets." This naming convention aids in identifying and managing these specific files.

### Config Load Priority

When the configuration files are loaded by LinuxGSM, they adhere to a specific order. Initially, settings are fetched from `_default.cfg`, followed by `common.cfg`, and finally `instance.cfg`. As a result, any setting specified in `instance.cfg` will take precedence over the same setting in `common.cfg`, which, in turn, overrides the setting in `_default.cfg`. This hierarchical loading ensures that settings become increasingly specific, with instance configurations having the highest priority.

#### LinuxGSM config load order

```
_default.cfg -> common.cfg -> instance.cfg
```

## How to Use

### Simple Configuration

This configuration fits most scenarios, where you have a simple installation with only one instance.

1. Browse to the `config-lgsm` directory

```
cd lgsm/config-lgsm/
```

1. Use `ls` to list the directory contents and find the name of your instance.cfg.
2. Use `cat` or `nano` to see the contents of `_default.cfg` .

```
cat _default.cfg
```

1. Copy the individual settings you want to change to `instance.cfg`

{% hint style="info" %}
It is recommended you only copy the settings you want to change from `_default.cfg` into `instance.cfg`. If any settings in \_default.cfg are updated with a new release of LinuxGSM they may not be picked up if all the settings have been copied.
{% endhint %}

### Multiple Instances Configuration

This configuration is useful for [multiple instances](../features/multiple-game-servers.md#single-installation-with-multiple-instances).

1. Browse to the `config-lgsm` directory

```
cd lgsm/config-lgsm/
```

1. Use `ls` to list the directory contents.
2. Use `cat` or `nano` to see the contents of `_default.cfg` .
3. Copy any settings you want to apply to _all_ instances to `common.cfg`.

{% hint style="info" %}
It is recommended you only copy the settings you want to change from `_default.cfg` into `instance.cfg`. If any settings in \_default.cfg are updated with a new release of LinuxGSM they may not be picked up if all the settings have been copied.
{% endhint %}

1. Copy any settings you want to apply to a specific instance to its `instance.cfg`.

```
csgoserver.cfg
csgoserver-2.cfg
```

## Examples

#### Example 1

Load `de_nuke` as default map on `csgoserver`:

```
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
csgoserver.cfg: defaultmap="de_nuke"
```

#### Example 2

Load `cs_office` as default map on `csgoserver`:

```
_default.cfg: defaultmap="de_dust2"
common.cfg: defaultmap="cs_office"
csgoserver.cfg: NOT SET
```

#### Example 3

Load `de_dust2` as default map on `csgoserver`:

```
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
csgoserver.cfg: NOT SET
```

#### Example 4

Load `de_nuke` as default map on `csgoserver` instance and `de_inferno` on `csgoserver-2` instance:

```
_default.cfg: defaultmap="de_dust2"
common.cfg: defaultmap="de_inferno"
csgoserver.cfg: defaultmap="de_nuke"
csgoserver-2.cfg: NOT SET
```

#### Example 5

Load `de_nuke` as default map on `csgoserver` instance and `cs_office` on `csgoserver-2` instance:

```
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
csgoserver.cfg: defaultmap="de_nuke"
csgoserver-2.cfg: defaultmap="cs_office"
```
