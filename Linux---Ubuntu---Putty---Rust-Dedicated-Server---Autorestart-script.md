Hello.

We have bought a dedicated server few days ago. 

We are french speaking but can understand english.

We installed Ubuntu Server 16.04 "Xenial Xerus" LTS (64bits) on our So you start Game 1 dedicated server.

We have installed putty to access SSH console. 

Then we followed tuto to install Rust ( we have put 2 rust servers on one machine ).

We succeeded to make both servers work. We can connect, play, save, install plugins, manually restart the servers.

We wanted to schedule 2 restarts each day on both servers, and we saw that the plugin we use : Timedexecute 

`"17:00:00": "say <color=orange>Is Autorestarting in</color> 1 hour",
    "17:30:00": "say <color=orange>Is Autorestarting in</color> 30 minutes",
    "17:45:00": "say <color=orange>Is Autorestarting in</color> 15 minutes",
    "17:50:00": "say <color=red>Is Autorestarting in</color> 10 minutes",
    "17:54:59": "say <color=red>Is Autorestarting in</color> 5 minutes",
    "17:59:00": "say <color=red>Is Autorestarting in</color> 1 minute",
    "17:59:57": "say <color=red>The server is now restarting.</color>",
    "17:59:58": "server.save",
    "18:00:00": "restart 0"`

So everything was working fine : we have notifications on the screen, and when it comes to 18:00:00 the server is stopping but not AUTOMATICALLY RESTARTING.

and that is the problem we have.

We were told to start the rust server with a .sh (oxide file) to allow the timedexecute to take the autorestart into consideration but we cannot do it, we don t know how to do. 

We tried this : 

`#!/bin/sh
clear
while :
do
    echo "Starting server...\n"
    exec ./RustDedicated -batchmode -nographics \
    -server.ip X.X.X.X \
    -server.port 28025 \
    -rcon.ip X.X.X.X.X\
    -rcon.port 28026 \
    -rcon.password "XXXXXXXXX" \
    -server.maxplayers 150 \
    -server.hostname "[EU] DEFCON X4 |NEW DEDI| Wipe 12/05" \
    -server.identity "rust-server" \
    -server.level "Procedural Map" \
    -server.seed 2017014 \
    -server.worldsize 3500 \
    -server.saveinterval 1800 \
    -server.globalchat true \
    -server.description "XXXXXXXXXX" \
    -server.headerimage "http://www.eudefcon.eu/wp-content/uploads/2017/05/Defcon_x4_Headerimage.png" \
    -server.url "http://www.eudefcon.eu/index.php/en/homepage/"
    echo "\nRestarting server...\n"
done`

The server is starting, but when we arrive at the line EasyAntiCheat we have the message : Easy AntiCheat Shutting Down.

`5:08:42) | server.description: "Powered by Oxide"
(15:08:42) | server.url: "http://oxidemod.org/"
(15:08:42) | server.headerimage: "http://i.imgur.com/xNyLhMt.jpg"
(15:08:42) | Initializing 134 stability supports
(15:08:43) | Couldn't initialize Steam Server (2760165935)
(15:08:43) | Updating Rust:IO ...
(15:08:44) | [MagicLoot] Loaded 326 item limits from /data/MagicLoot.json
(15:08:44) | [MagicLoot] Loaded 19 components from /config/MagicLoot.json
(15:08:44) | [MagicLoot] Loaded at x4 vanilla rate | components rate x4  [Extra Loot: False | X Only Components: False]
(15:08:44) | [MagicLoot] Repopulated 754 loot containers.
(15:08:44) | [Timed Execute] The RealTime timer has started
(15:08:44) | [Timed Execute] The Timer-Once timer has started
(15:08:44) | Server startup complete
(15:08:44) | Unloaded plugin Rust:IO for Oxide v2.13.0 by playrust.io / dcode
(15:08:44) | Unloaded plugin Crafting Controller v2.4.7 by Mughisi
(15:08:44) | Unloaded plugin Gathering Manager v2.2.4 by Mughisi
(15:08:44) | Unloaded plugin Kits v3.2.6 by Reneb
(15:08:44) | Unloaded plugin MagicLoot v0.1.10 by Norn
(15:08:44) | Unloaded plugin QuickSmelt v3.0.2 by Wulf/Fujikura
(15:08:44) | Unloaded plugin SharedDoors v0.7.6 by dbteku
(15:08:44) | Unloaded plugin Stack Size Controller v1.9.4 by Canopy Sheep
(15:08:44) | Unloaded plugin Timed Execute v0.7.1 by PaiN
(15:08:44) | Unloaded plugin Vanish v0.3.7 by Wulf/lukespragg
(15:08:44) | EasyAntiCheat Shutting Down`


We don't know what to do ? ( we are not pro with Linux ).

Thanks in advance if you can give us some steps to follow. 



