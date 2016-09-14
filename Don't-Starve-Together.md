**_WORK IN PROGRESS (regarding dstserver branch)_**

## Introduction
A Don't Starve Together server consists of **clusters** and **shards**. 

One cluster can contain multiple shards. A shard is basically a map/level. Multiple shards are connected by cave entrances/exits found on the map. These are functioning as portals to allow players to travel between actual game servers. 

**Each shard (level of the world) has to be run as an individual server instance.**

## Single-Shard
By default the cluster will be single-sharded. So you only need one server but you will also only have one map.

server script settings:
```bash
multishard="false"
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

dstserver1 (this will be the master shard with an overworld as level):
```bash
# Installation Variables
multishard="true"
slave="false"
shard="Master" 
cluster="Cluster_1"
cave="false"

# Start Variables
port="11000"
steamauthenticationport="8768"
steammasterserverport="27018"
```

dstserver2 (this will be the slave shard with a cave as level):
```bash
# Installation Variables
multishard="true"
slave="true"
shard="Caves" 
cluster="Cluster_1"
cave="true"

# Start Variables
port="11001"
steamauthenticationport="8769"
steammasterserverport="27019"
```

**Set all installation variables BEFORE running the `./dstserver1/2 install` commands.** You also should not change them afterwards. Feel free to change these settings but make sure that you set them to the same clusters. 

For clarity reasons I recommend naming the master shard "Master".

Lastly you have to start both servers. The order does not matter because the slave server will auto-retry to connect to the master server.


#### Guides / Documentations:
* [Quick Setup](http://forums.kleientertainment.com/topic/64441-dedicated-server-quick-setup-guide-linux/)
* [Server Settings](http://forums.kleientertainment.com/topic/64552-dedicated-server-settings-guide/)
* [Command Line Options](http://forums.kleientertainment.com/topic/64743-dedicated-server-command-line-options-guide/)
* [Understanding Shards and Migration Portals](http://forums.kleientertainment.com/topic/59174-understanding-shards-and-migration-portals/)

## OLD:
Here are the Dont Starve Together install guides. A Linux one is included. The setup is quite complicated but should work with LGSM with some configuration. 

http://steamcommunity.com/id/ToNiO44/myworkshopfiles/?section=guides&appid=322330