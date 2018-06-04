# System requirements

* RAM: 4GB-12GB, Increases depending upon map size
* CPU: Duel core 3.4GHz, Rust is monothread
* Bandwidth: 10mbps upload

> note The server autosave can cause lag, depending on the CPU and disk speed.

# Modded server with Oxide

LinuxGSM supports downloading, updating, or removing Oxide.

```
./rustserver mods-install
```

# Useful Links

## General Information
https://developer.valvesoftware.com/wiki/Rust_Dedicated_Server

## Oxide Support
http://oxidemod.org/threads/setting-up-a-rust-server-with-linux-and-lgsm.16528/

## Rusty
* Server RCON administration tool 
http://oxidemod.org/resources/rusty-server-rcon-administration-tool.53/

# Rust Server with LinuxGSM Video tutorial
A quick tour of Rust special features, and install guide for Rust and Oxide.

https://www.youtube.com/watch?v=6GaoyPeN71g

If you need more help, here is a video that shows a bit more into depth how to use LinuxGSM, how the directory structure works, it also explains the basics of a Rust Server and other stuff, that's why it's 20 minutes long, otherwise, if you're experienced, you can get your server up and running in around 5 minutes without any mods.

https://www.youtube.com/watch?v=eFH9Qj-hUOM

# Rust Console
Rust has no console to display useful information. Instead you need to monitor the server logs or RCON login to display real time info.
````bash
tail -f log/server/rust-server*.log`
````

# Install Oxide
Oxide is an API allowing you to run mods for you Rust server.

LinuxGSM now handles the install of Oxide for Rust, with `mods-install` and `mods-update` commands.

````bash
./rustserver mods-install
````

If a Rust update has been released, then an Oxide update will soon follow. To update Oxide, you can then run:

````bash
./rustserver mods-update
````

## Install Oxide addons

To install Oxide addons place them into  the `serverfiles/oxide/plugins` directory.
This will cause them to load automatically when starting the server.

If you need to edit any addon configs, they will be located in `serverfiles/oxide/config`.

To update and addon without restarting the server, you'll need to reload the addon with an RCON command.
```
oxide.reload PluginName
```
# RCON
## Send RCON commands:

RCON is the protocol used to send commands to your server. You will need a tool to use it. Here are 3 of them:
* Rusty: http://oxidemod.org/resources/rusty-server-rcon-administration-tool.53/
* Rustadmin: https://www.rustadmin.com/ (supports both rconweb=1 and rconweb=0)
* Facepunch web tool: http://facepunch.github.io/webrcon/#/home

To use software like Rusty, you need to alter LinuxGSM config and change `rconweb="0"`. 
To use Facepunch tool or Rustadmin, you can leave it at default `rconweb="1"`

> Note: Facepunch web tool currently don't accept domain names, you need to enter server IP.

## Essential RCON Commands

```
save ; will save the server state (useful before a stop or restart)
oxide.reload PluginName ; will reload a plugin after updating it
ownerid STEAMID64 "Nickname" "Reason" ; to add an owner
moderatorid STEAMID64 "Nickname" "Reason" ; to add a moderator
server.writecfg ; will save config changes, including new admins
```

> Note: append `server.writecfg` after adding an admin, and player needs to reconnect the server in order for it to be applied. 


# Avoid a security breach and allow you to run multiple servers

By default, a user can see all started processes from other users, which is bad, but also their start parameters, which is pretty dangerous. Those start parameters can contain sensitive information, such as RCON password, Steam API keys, GSLTokens...
Upon start, a Rust dedicated server is checking if the process name started by any user, and will prevent you from running it again if it finds it, displaying "Player is already running".

To avoid that, run:

````bash
mount -o remount,rw,hidepid=2 /proc
````

And to keep the changes upon machine reboot:

````bash
nano /etc/fstab
# Here are the modification to apply to the "proc" line
proc    /proc    proc    defaults,hidepid=2    0    0
````

You still need to make one user per server, change ports, and repeat the install process. (See https://github.com/GameServerManagers/LinuxGSM/wiki/Multiple-Servers for more info)


# Server Wipe
````bash
./rustserver wipe
````

auto wipe
````bash
echo y | ./rustserver wipe
````