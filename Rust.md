"Native" Linux support for Rust is back since February 2016 ! https://twitter.com/garrynewman/status/700658567641231360

# System requirements

## RAM
A Rust game server uses roughly 4GB to 12GB RAM, depending on the map size.  
LinuxGSM will warn you if your server has less than 4GB RAM available.

## CPU
will constantly use around 50% of one core from a Xeon E5-1650V3 (6 cores 12 threads, 3.8Ghz), or around 30% of one core from an I7 4870K, regardless of the amount of people connected. As with most game servers, it seems like Rust is mono threaded.

## Bandwidth
10mbps upload is reccomended

## Other notes
The server autosave can cause lag, depending on the CPU and disk speed. An server will a decent CPU and SSD can help.

## Conclusion
Rust does not require a server with a high amount of cores @1,2Ghz, prefer a quad/hexa core @+3,3Ghz, check benchmarks before choosing your server. CPU: good monothread performance ;RAM: 12-16GB and more; avoid VPS.

# Linux Distribution
You will need Glibc greater or equal to v2.15 (more info https://github.com/dgibbs64/linuxgsm/wiki/Glibc )

# Modded server with Oxide

In this guide, we're going to go through the Rust install process, correcting your system to handle multiple Rust servers, installing Oxide and keeping it updated easily.

> UPDATE 2017-01-29: LinuxGSM now supports downloading, updating, or removing Oxide! Run [[update-functions]] command to get the new feature!

# Useful Links

## Manual Installation and general information
* If you wish to use the manual way, @UltimateByte has updated the Valve Rust wiki (that still needs some work): https://developer.valvesoftware.com/wiki/Rust_Dedicated_Server

## LinuxGSM Installation
* If you wish to use LinuxGSM, grab the script provided here: https://gameservermanagers.com/lgsm/rustserver/

## Oxide Support
http://oxidemod.org/threads/setting-up-a-rust-server-with-linux-and-lgsm.16528/

## LinuxGSM Support
* See https://github.com/GameServerManagers/LinuxGSM/wiki/Support

## Oxide for Linux
* Oxide for linux : wget https://github.com/OxideMod/Snapshots/raw/master/Oxide-Rust.zip
Rusty Rcon Tool

## Rusty
* Server RCON administration tool http://oxidemod.org/resources/rusty-server-rcon-administration-tool.53/

# Rust Server with LinuxGSM Video tutorial

Here is a quick tour of Rust special features, and install guide for Rust and Oxide.

https://www.youtube.com/watch?v=6GaoyPeN71g

If you need more help, here is a video that shows a bit more into depth how to use LinuxGSM, how the directory structure works, it also explains the basics of a Rust Server and other stuff, that's why it's 20 minutes long, otherwise, if you're experienced, you can get your server up and running in around 5 minutes without any mods.

https://www.youtube.com/watch?v=eFH9Qj-hUOM


# LinuxGSM Tutorial

## 0) Make sure you have all the dependencies

And make sure you match the distro requirement by carefully reading instructions at: https://gameservermanagers.com/lgsm/rustserver/

## 1) Make a new user and login to it

As root, do:

````
adduser rustserver
[...]
su - rustserver
````

## 2) Get LinuxGSM and make it executable

````bash
wget https://gameservermanagers.com/dl/rustserver
chmod +x rustserver
````

## 3) Run the installer and follow the instructions

````bash
./rustserver install
````

## 4) Edit rustserver to fit your needs

You'd better use nano or vim, but you could also use a text editor like notepad++, which is way less convenient. If you need help about what to configure, watch the video.

````bash
nano rustserver
````

## 5) Edit server.cfg

````bash
nano serverfiles/server/rust-server/cfg/server.cfg
````

## 6) Make sure everything is alright

Start your server

````bash
cd ~
./rustserver start
````

Then check your logs located in
````bash
log/server/
````

Since Rust have no console, you can use this workaround to display the log in real time:
````bash
tail -f log/server/rust-server*.log`
````

Since Rust don't allow setting a custom log location, the log file will be called game-{FULL-CURRENT-DATE}.log to not be erased on every restart and will be moved to log/server upon any server start/restart and a new one will be created.

Note: The Rust console is empty under Linux. You'll have to use an RCON tool and/or watch your logs. 

## 7) Install Oxide

As a reminder, Oxide is an API allowing you to run mods for you Rust server.

LinuxGSM now handles Oxide for Rust naively, with mods-install and mods-update commands.

````bash
./rustserver mods-install
rustoxide
````

Then you'd better check your logs again after restarting the server to check that Oxide is loading properly.

If a Rust update has been released, then an Oxide update will soon follow. To update Oxide, you can then run:

````bash
./rustserver mods-update
````

## 8) Install Oxide addons

Just put them into `serverfiles/server/rust-server/oxide/plugins`
They will load automatically.  
If you need to edit their configs, it will be located in : `serverfiles/server/rust-server/oxide/config`  
If you updated an addon and wish to reload it without restarting the server, you'll need to input it in an RCON tool. Once you've got it, run :
```
oxide.reload PluginName
```

## 9) Send RCON commands:

RCON is the protocol used to send commands to your server. You will need a tool to use it. Here are 3 of them:
* Rusty: http://oxidemod.org/resources/rusty-server-rcon-administration-tool.53/
* Rustadmin: https://www.rustadmin.com/ (supports both rconweb=1 and rconweb=0)
* Facepunch web tool: http://facepunch.github.io/webrcon/#/home

To use an external software like Rusty, you need to alter `rustserver` script with `rconweb="0"`. To use Facepunch tool or Rustadmin, you can leave it at default `rconweb="1"`

Note: Facepunch web tool currently don't accept domain names, you need to enter server IP.

If you can't remember the RCON port you set or password (that you MUST change), just use:
````bash
./rustserver details
````

**Essential commands**

```
save ; will save the server state (useful before a stop or restart)
oxide.reload PluginName ; will reload a plugin after updating it
ownerid STEAMID64 "Nickname" "Reason" ; to add an owner
moderatorid STEAMID64 "Nickname "Reason" ; to add a moderator
server.writecfg ; will save config changes, including new admins
```

Note: append `server.writecfg` after adding an admin, and player needs to reconnect the server in order for it to be applied. 

## 10) Avoid a security breach and allow you to run multiple servers

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

Of course, you still need to make one user per server, change ports, and repeat the install process. (See https://github.com/GameServerManagers/LinuxGSM/wiki/Multiple-Servers for more info)

## 11) Setup automated tasks (reboot, update...)

You will need to use Linux Cronjobs. For more information, see https://github.com/GameServerManagers/LinuxGSM/wiki/Cronjobs

Basically, I advise you to setup root cronjobs.
The syntax for root cronjobs is (replace things between <> by the actual value)

````bash
* * * * * su - <username> -c '/home/<username>/rustserver <command>' > /dev/null 2>&1
````

Example for a restart every day at 5:
Login to Root (su command), then do: 

````bash
crontab -e
0 5 * * * su - rust -c '/home/rust/rustserver restart' > /dev/null 2>&1

# save and exit (ctrl +x, y, enter if using nano)
````

You can run a monitor cronjob every few minutes to make sure your server is up and runing.
````bash
*/3 * * * *  su - rust -c '/home/rust/rustserver monitor' > /dev/null 2>&1
````

## 12) Updating Rust

Just run
````bash
./rustserver update
````

If needed, run
````bash
./rustserver validate
````

To wipe the server run
````bash
./rustserver wipe
````

To update Oxide, that your previously installed with LinuxGSM, run
````bash
./rustserver mods-update
````

## Special Thanks : 
* UltimateByte for Rust support into LinuxGSM and documentation
* Wulf and Oxide team for enlightening about Rust and Oxide
* [Daniel Gibbs](https://twitter.com/dangibbsuk), Founder of LinuxGSM, for his help making this work
* CedarLUG, LinuxGSM Support, for his help dealing with Rust's weirdness