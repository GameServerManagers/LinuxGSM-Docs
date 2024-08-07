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

~/.klei/DoNotStarveTogether/Cluster_1/Master/server.ini

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

~/.klei/DoNotStarveTogether/Cluster_1/Caves/server.ini

```text
[NETWORK]
server_port = 11001

[STEAM]
authentication_port = 8769
master_server_port = 27019
```

If you want to Caves and Overworld to display on the same server, you also to change the cluster.ini, otherwise it will run two instances, one with the Overworld and another with the Caves:

~/.klei/DoNotStarveTogether/Cluster_1/cluster.ini

```lua
[SHARD]
shard_enabled = true
```

**Set all installation variables BEFORE running the** `./dstserver-[1,2] install` **commands.** Feel free to change these settings but make sure that you set them to the same clusters. You also should not change them afterwards.

For clarity it is recommended recommend naming the master shard _**Master**_.

Lastly you have to start both servers. The order does not matter because the slave server will auto-retry connecting to the master server which is listening.

## Guides / Documentations

-   [Quick Setup](http://forums.kleientertainment.com/topic/64441-dedicated-server-quick-setup-guide-linux/)
-   [Server Settings](http://forums.kleientertainment.com/topic/64552-dedicated-server-settings-guide/)
-   [Command Line Options](http://forums.kleientertainment.com/topic/64743-dedicated-server-command-line-options-guide/)
-   [Understanding Shards and Migration Portals](http://forums.kleientertainment.com/topic/59174-understanding-shards-and-migration-portals/)
