# Dont Starve Together

## Authentication Token

Don't Starve Together server requires an Authentication Token.

1. Go to the Klei website [https://accounts.klei.com](https://accounts.klei.com).
2. After logging into your account [visit this page](https://accounts.klei.com/account/game/servers?game=DontStarveTogether) to get your game server authentication token.
3. Enter a friendly name for your server and copy the access token and paste it into the file `cluster_token.txt`.

You can quickly do this by running the following command, replacing `[AUTHTOKEN]` with your authentication token.

```bash
echo '[AUTHTOKEN]' > ~/.klei/DoNotStarveTogether/[CLUSTER]/cluster_token.txt
```

## Clusters and Shards

A Don't Starve Together server consists of **clusters** and **shards**.

One cluster can contain multiple _shards_. A _shard_ is simply a map/level. Multiple _shards_ are connected by cave entrances/exits found on the map. These are functioning as portals to allow players to travel between actual game servers.

{% hint style="info" %}
Each shard \(level of the world\) has to be run as an individual game server instance.
{% endhint %}

### Single-Shard

By default, the cluster will be single-sharded. So you only need one server but you will also only have one map.

Default start parameter setting:

```bash
sharding="false"
```

### Multi-Shard

Take a look at [Multiple-Servers](https://docs.linuxgsm.com/features/multiple-game-servers) to get a general idea of how to create multiple game servers.

There are two types of shards:

1. **master shard**: the shard you enter when joining the server / the shard/server you have to join \(**one** per cluster\)
2. **slave shard**: shard that will connect to the master \(arbitrary number per cluster\)

In this example, we will only use two shards, one overworld shard and one cave shard, on the same machine using the same installation. If you want to use more shards or run the shards on different machines, take a look at the guides mentioned at the bottom. First of all we need two scripts:

```text
./dstserver-1
./dstserver-2
```

#### Server \#1

_**dstserver-1**_ will be the _master shard_ with an overworld as level.

```bash
## Predefined Parameters
sharding="true"
master="true"
shard="Master" 
cluster="Cluster_1"
cave="false"
```

~/.klei/DoNotStarveTogether/Cluster\_1/Master/server.ini

```text
[NETWORK]
server_port = 11000

[STEAM]
authentication_port = 8768
master_server_port = 27018
```

#### Server \#2

dstserver-2 \(this will be the slave shard with a cave as level\):

```bash
## Predefined Parameters
sharding="true"
master="false"
shard="Caves" 
cluster="Cluster_1"
cave="true"
```

~/.klei/DoNotStarveTogether/Cluster\_1/Caves/server.ini

```text
[NETWORK]
server_port = 11001

[STEAM]
authentication_port = 8769
master_server_port = 27019
```

If you want to Caves and Overworld to display on the same server, you also to change the cluster.ini, otherwise it will run two instances, one with the Overworld and another with the Caves:

~/.klei/DoNotStarveTogether/Cluster\_1/cluster.ini

```lua
[SHARD]
shard_enabled = true
```

**Set all installation variables BEFORE running the** `./dstserver-[1,2] install` **commands.** Feel free to change these settings but make sure that you set them to the same clusters. You also should not change them afterwards.

For clarity it is recommended recommend naming the master shard _**Master**_.

Lastly you have to start both servers. The order does not matter because the slave server will auto-retry connecting to the master server which is listening.

### Caves

Setting `cave="true"` on a shard is all that is required to turn it into an actual cave, LinuxGSM handles the rest automatically during install.

{% hint style="info" %}
`cave` only affects world generation. It has no effect unless `sharding="true"` and `shard` is set to a unique name for that instance, as shown in the `dstserver-2` example above.
{% endhint %}

When a server is installed with `cave="true"`, LinuxGSM writes the following file for you:

~/.klei/DoNotStarveTogether/Cluster\_1/Caves/worldgenoverride.lua

```lua
return { override_enabled = true, preset = "DST_CAVE", }
```

This is what tells the game to generate an underground cave map for that shard instead of a normal overworld. Without it, a "Caves" shard would just generate a second overworld map. Since this file is only written on install, changing `cave` on an already-installed shard requires a fresh install (or a reinstall) of that instance to regenerate the world with the new preset.

## Installing Mods

LinuxGSM does not install or manage Don't Starve Together mods automatically, this has to be done manually in three steps.

### 1. Enable mods for download

Add each mod's Steam Workshop ID to `dedicated_server_mods_setup.lua` so the dedicated server downloads it from the Workshop.

~/serverfiles/mods/dedicated_server_mods_setup.lua

```lua
ServerModSetup("378160973")
ServerModSetup("some-other-workshop-id")
```

Run `./dstserver update` (or `install`) afterwards so the mods get downloaded.

### 2. Enable mods per shard

Each shard (Master and Caves) needs its own `modoverrides.lua` listing which mods are enabled for that shard.

~/.klei/DoNotStarveTogether/Cluster\_1/Master/modoverrides.lua

```lua
return {
  ["workshop-378160973"] = { enabled = true },
  ["workshop-some-other-workshop-id"] = { enabled = true },
}
```

{% hint style="warning" %}
Note the `workshop-` prefix before the ID in `modoverrides.lua`. This is different from `dedicated_server_mods_setup.lua`, which uses the bare ID.
{% endhint %}

Copy the same file into the `Caves` shard directory if you want the mod active there too, most world/gameplay mods need to be enabled on both shards to behave consistently.

### 3. Configure mod settings (optional)

Some mods expose extra configuration options (difficulty, spawn rates, etc). The easiest way to generate a correctly formatted `modoverrides.lua` with these settings is to temporarily host a non-dedicated client server with the same mods enabled, configure the mods through the in-game mod options UI, generate the world once, then copy the resulting `modoverrides.lua` from that client's save folder over to both the Master and Caves shard directories on the dedicated server.

## Guides / Documentations:

* [Quick Setup](http://forums.kleientertainment.com/topic/64441-dedicated-server-quick-setup-guide-linux/)
* [Server Settings](http://forums.kleientertainment.com/topic/64552-dedicated-server-settings-guide/)
* [Command Line Options](http://forums.kleientertainment.com/topic/64743-dedicated-server-command-line-options-guide/)
* [Understanding Shards and Migration Portals](http://forums.kleientertainment.com/topic/59174-understanding-shards-and-migration-portals/)

