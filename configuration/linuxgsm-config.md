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
Secret configs are not encrypted, but a place to store sensetive info away from other configs.
{% endhint %}

The secret configs are a place to put sensitive information such as steam login details away from the main config files. This is done to allow server admins to backup their configs while excluding sensitive information. This is particularly useful for admins who want to create a version-controlled skeleton configuration using git that they might want to make public.

It is important to know that the secret config is NOT encrypted or any more secure than other configs.

A secret config can be identified with the word `secrets` prepended to the front of the config name.

### Config Load Priority

When LinuxGSM is loading the configs they will load in order. First taking settings from `_default.cfg` then `common.cfg` and finally `instance.cfg`. This means that any setting set in `instance.cfg` will override that setting in `common.cfg` which in turn will override the setting in `_default.cfg`.

#### LinuxGSM config load order

```text
_default.cfg -> common.cfg -> instance.cfg
```

## How to Use

### Simple Configuration

This configuration fits most scenarios, where you have a simple installation with only one instance.

1. Browse to the `config-lgsm` directory

```text
cd lgsm/config-lgsm/
```

2. Use `ls` to list the directory contents and find the name of your instance.cfg.

3. Use `cat` or `nano` to see the contents of `_default.cfg` .

```text
cat _default.cfg
```

4. Copy the individual settings you want to change to `instance.cfg`

{% hint style="info" %}
It is recommended you only copy settings you want to change from `_default.cfg` into `instance.cfg`. If any settings in \_default.cfg are updated with a new release of LinuxGSM they may not be picked up if all the settings have been copied.
{% endhint %}

### Multiple Instances Configuration

This configuration is useful for [multiple instances](../features/multiple-game-servers.md#single-installation-with-multiple-instances).

1. Browse to the `config-lgsm` directory

```text
cd lgsm/config-lgsm/
```

2. Use `ls` to list the directory contents.

3. Use `cat` or `nano` to see the contents of `_default.cfg` .

4. Copy any settings you want to apply to _all_ instances to `common.cfg`.

{% hint style="info" %}
It is recommended you only copy settings you want to change from `_default.cfg` into `instance.cfg`. If any settings in \_default.cfg are updated with a new release of LinuxGSM they may not be picked up if all the settings have been copied.
{% endhint %}

5. Copy any settings you want to apply to a specific instance to its `instance.cfg`.

```text
csgoserver.cfg
csgoserver-2.cfg
```

## Examples

#### Example 1

Load `de_nuke` as default map on `csgoserver`:

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
csgoserver.cfg: defaultmap="de_nuke"
```

#### Example 2

Load `cs_office` as default map on `csgoserver`:

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: defaultmap="cs_office"
csgoserver.cfg: NOT SET
```

#### Example 3

Load `de_dust2` as default map on `csgoserver`:

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
csgoserver.cfg: NOT SET
```

#### Example 4

Load `de_nuke` as default map on `csgoserver` instance and `de_inferno` on `csgoserver-2` instance:

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: defaultmap="de_inferno"
csgoserver.cfg: defaultmap="de_nuke"
csgoserver-2.cfg: NOT SET
```

#### Example 5

Load `de_nuke` as default map on `csgoserver` instance and `cs_office` on `csgoserver-2` instance:

```text
_default.cfg: defaultmap="de_dust2"
common.cfg: NOT SET
csgoserver.cfg: defaultmap="de_nuke"
csgoserver-2.cfg: defaultmap="cs_office"
```

