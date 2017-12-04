## Introduction
A Don't Starve Together server consists of **clusters** and **shards**. 

One cluster can contain multiple shards. A shard is basically a map/level. Multiple shards are connected by cave entrances/exits found on the map. These are functioning as portals to allow players to travel between actual game servers. 

>note: Each shard (level of the world) has to be run as an individual server instance.

## Single-Shard
By default the cluster will be single-sharded. So you only need one server but you will also only have one map.

Default script settings:

```bash
sharding="false"
```
## Multi-Shard
First of all take a look at [Multiple-Servers](https://github.com/GameServerManagers/LinuxGSM/wiki/Multiple-Servers) to get a general idea on how to create multiple game servers.

There are two types of shards:

1. **master shard**: the shard you enter when joining the server / the shard/server you have to join (**one** per cluster)
2. **slave shard**: shard that will connect to the master (arbitrary number per cluster)

In this example we will only use two shards, one overworld shard and one cave shard, on the same machine using the same installation. If you want to use more shards or run the shards on different machines, take a look at the guides mentioned at the bottom.
First of all we need to scripts:

```
./dstserver1
./dstserver2
```

### Server #1

dstserver1 (this will be the master shard with an overworld as level):
```bash
# Installation Variables
sharding="true"
master="true"
shard="Master" 
cluster="Cluster_1"
cave="false"
```

~/.klei/DoNotStarveTogether/Cluster_1/Master/server.ini
```ini
[NETWORK]
server_port = 11000

[STEAM]
authentication_port = 8768
master_server_port = 27018
```

### Server #2

dstserver2 (this will be the slave shard with a cave as level):
```bash
# Installation Variables
sharding="true"
master="false"
shard="Caves" 
cluster="Cluster_1"
cave="true"
```

~/.klei/DoNotStarveTogether/Cluster_1/Caves/server.ini
```ini
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

**Set all installation variables BEFORE running the `./dstserver1/2 install` commands.**  Feel free to change these settings but make sure that you set them to the same clusters. You also should not change them afterwards. If you have multiple clusters on one machine with the same shard names, you have to modify the servicename because `servicename="dst-server-${shard}"`
(The shard name is used to differentiate service names. e.g. `servicename="dst-server-${cluster}-${shard}"`).

For clarity reasons I recommend naming the master shard "Master".

Lastly you have to start both servers. The order does not matter because the slave server will auto-retry connecting to the master server which is listening.


#### Guides / Documentations:
* [Quick Setup](http://forums.kleientertainment.com/topic/64441-dedicated-server-quick-setup-guide-linux/)
* [Server Settings](http://forums.kleientertainment.com/topic/64552-dedicated-server-settings-guide/)
* [Command Line Options](http://forums.kleientertainment.com/topic/64743-dedicated-server-command-line-options-guide/)
* [Understanding Shards and Migration Portals](http://forums.kleientertainment.com/topic/59174-understanding-shards-and-migration-portals/)