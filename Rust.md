"Native" Linux support for Rust is back since February 2016 ! https://twitter.com/garrynewman/status/700658567641231360

That allowed us to add a Rust Server Script into LGSM.

# Modded server with Oxide


## System requirements

### RAM
The Rust game server process will take up from 6 to 10GB RAM, depending on your map size.
For that matter, LGSM warns you if you have less than 4GB available.

### CPU
It will also use constantly 50-65% of  one core from a Xeon E5-1650V3 (6 cores 12 threads, 3.8Ghz), regardless of the amount of people connected and with very few constructions on it. As most game servers, it seems like it's mainly monothread, so you'd better have some good monothread performance.

### Bandwidth
Bandwidth shouldn't be an issue, aim for a 10-15mb/s+ connection minimum

### Other notes
The server autosave can cause lags, depending on your CPU and disk speed.
It is highly recommended a dedicated server is used with Rust because of it's high system requirements.

### Conclusion
Don't take a stupid server with 150 cores @1,2Ghz, prefer a quad/hexa core @3,3Ghz+, check benchmarks before choosing your server. CPU : good monothread performance ; RAM : 12-16GB and more ; avoid VPS.


## Linux Distribution
You will need Glibc greater or equal to v2.15 (more info https://github.com/dgibbs64/linuxgsm/wiki/Glibc )

So you need :
* Ubuntu 12.04 LTS or greater
* Debian 8 or greater
* CentOS 7 or greater

## Useful Links

### Manual Installation and general information
* If you wish to use the manual way, i updated the Valve Rust wiki (that still needs some work) : https://developer.valvesoftware.com/wiki/Rust_Dedicated_Server

### LGSM Installation
* If you wish to use LGSM, grab the script provided here : http://gameservermanagers.com/lgsm/rustserver/

### Oxide Support
http://oxidemod.org/threads/setting-up-a-rust-server-with-linux-and-lgsm.16528/

### LGSM Support
* General support : https://steamcommunity.com/groups/linuxgsm/discussions
* Report a bug : https://github.com/dgibbs64/linuxgsm/issues

### Updater Script for Oxide
* https://github.com/UltimateByte/zip-updater

### Oxide for Linux
* Oxide for linux : wget https://github.com/OxideMod/Snapshots/raw/master/Oxide-Rust_Linux.zip
Rusty Rcon Tool
### Rusty
* Server RCON administration tool http://oxidemod.org/resources/rusty-server-rcon-administration-tool.53/

## Rust Server with LGSM Video tutorial

If you need some help, here is a video that shows how to use LGSM, it also explains the basics of a Rust Server, and other stuff, that's why it's 20 minutes long, otherwise, if you're experienced, you can get your server up and running in around 5 minutes without any mods.

https://www.youtube.com/watch?v=eFH9Qj-hUOM


# LGSM Tutorial

0) Make sure you have all the dependencies
And make sure you match the distro requirement by carefully reading instructions at : https://gameservermanagers.com/lgsm/rustserver/

1) Make a new user and login to it
As root, do :

```
adduser rust
[...]
login rust
```

2) Get LGSM and make it executable
```
wget http://gameservermanagers.com/dl/rustserver
chmod +x rustserver
```

3) Run the installer and follow the instructions

```
./rustserver install
```

4) Edit rustserver to fit your needs
You'd better use nano or vim, but you could also use a text editor line notepad++, which is way less convenient. If you need help about what to configure, watch the video.

```
nano rustserver
```

5) Edit server.cfg
Located in 
```
serverfiles/server/rust-server/cfg
```

6) Make sure everything is allright
Start your server

```
cd ~
./rustserver start
```

Then check your logs
```
cat serverfiles/game*.log
```

The log will be called game-{FULL-CURRENT-DATE}.log to not be erased on every restart.
Upon a server start (or restart), this log will be moved to log/server and a new one will be created. This is a workaround for the crappy default log management in Rust.

7) Install Oxide
You just have to download Oxide and extract it in a temp folder, then copy to your serverfiles folder, and clean the temp folder.
Of course, shut down the server first.
A good idea is to run a "save" command using Rusty or RCON before stopping your server. See 9) for more info.

Manual Way

```
./rustserver stop
mkdir temp && cd temp
wget https://github.com/OxideMod/Snapshots/raw/master/Oxide-Rust_Linux.zip
unzip Oxide-Rust_Linux.zip
rm Oxide-Rust_Linux.zip
cp * /home/rust/serverfiles
cd ~
./rustserver start
```

Setup the automated way
```
mkdir zip-updater && cd zip-updater
wget https://raw.githubusercontent.com/UltimateByte/zip-updater/master/zip-updater
chmod +x zip-updater
```
Then edit zip-updater accordingly
```
nano zip-updater
targetdir="/home/rust/serverfiles"
ziplinks="https://github.com/OxideMod/Snapshots/raw/master/Oxide-Rust_Linux.zip"
```

And ad the end, add after fn_prompt_continue : 
```
/home/rust/rustserver stop
```
 and at the very bottom : 
```
/home/rust/rustserver start
```

Example : 
```
# Running functions
echo ""
echo "Thanks for using this script made by UltimateByte"
fn_error_check
echo ""
echo "Start downloading or updating zips ?"
fn_prompt_continue
/home/rust/rustserver stop
fn_create_dirs
fn_dl_zip
fn_extract_zip
fn_lowercase
fn_copy
fn_rm_extractdir
fn_backup
fn_rm_zipsdir
fn_complete
/home/rust/rustserver start
```

Now any time there is an Oxide update, just run 
```
./zip-updater
```

Better check your logs again and check that Oxide is loading properly


8) Install Oxide addons
Just put them into ````````serverfiles/server/rust-server/oxide/plugins````````
They will load automatically.
If you need to edit their configs, it will be located in : ````````serverfiles/server/rust-server/oxide/config````````

If you updated an addon and wish to reload it without restarting the server, you'll need Rusty. Once you've got it, run :
```
oxide.reload PluginName
```

9) Connect in RCON using Rusty
Grab it here Rusty - Server RCON administration tool | Oxide
If you can't know your IP or domain name, you're a jerk.
If you can't remember the RCON port you set or password (that you MUST change), just use :
````````./rustserver details````````
Essential commands
```
save ; will save the server state (useful before a stop or restart)
oxide.reload PluginName ; will reload a plugin after updating it
server.writecfg ; to save config commands you ordered into Rusty, including new admins
ownerid STEAMID64 "Nickname" "Reason" ; to add an owner
moderatorid STEAMID64 "Nickname "Reason" ; to add a moderator
```

10) Avoid a security breach and allow you to run multiple servers
By default, a user can see all started processes from other users, which is bad, but also their start parameters, which is pretty dangerous. Those start parameters can contain sensitive information, such as RCON password, Steam API keys, GSLTokens...
Upon start, a Rust dedicated server is checking if the process name started in all users, and will prevent you from running it again if it finds it, displaying "Player is already running".
To avoid that, run

```
mount -o remount,rw,hidepid=2 /proc
```

And to keep the changes upon machine reboot

```
nano /etc/fstab

proc    /proc    proc    defaults,hidepid=2    0    0
```

Of course, you still need to make one user per server, change ports, and repeat the install process.

11) Setup automated reboot or any task
You will need to use Linux Cronjobs. For more information, see https://github.com/dgibbs64/linuxgsm/wiki/Automation

Basically, i advise you to setup root cronjobs.
The syntax for root cronjobs is (replace things between <> by the actual value)

```
0 5 * * * su - <username> -c '/home/<username>/rustserver <command>' > /dev/null 2>&1
```

Example for a restart every day at 5 :
Login to Root, then do : 

```
su
crontab -e
0 5 * * * su - rust -c '/home/rust/rustserver restart' > /dev/null 2>&1

save and exit (ctrl +x, y, enter)
```

You can run a monitor cronjob every few minutes to make sure your server is up and runing.
```
*/3 * * * *  su - rust -c '/home/rust/rustserver monitor' > /dev/null 2>&1
```

12) Updating Rust
Just run
```
./rustserver update
```
If needed, run
```
./rustserver validate
```
Then update oxide once the new version is released. If you followed this guide entirely :
```
./zip-updater/zip-updater
```

## Special Thanks :
* Wulf and Oxide team
* Daniel Gibbs, Founder and main dev from LGSM Daniel Gibbs https://twitter.com/dangibbsuk
* CedarLUG, LGSM Support
