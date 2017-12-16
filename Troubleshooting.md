This guide should cover a wide range of issues, but some might be more complicated than that. If you need further assistance, please make sure you read the [[Support]] to know the right place to reach us and what information to provide in order for us to be able to help you.

# Installation issues

Your game server might not install for many reasons, mainly user based ones, and some distro based.
Make sure you answer "yes" to any of these questions.

## User and permissions

* Did you create a dedicated user for your server?
* Are you running the script as the right user? Check command: `whoami`
* Does the user running the script owns its current directory? Check command: `ls -al .`, see [[File Ownership]]
* Does the user have the right permissions on its directories? See [[Permissions]]

## Dependencies

* Did you install required packages (dependencies) as game page on https://gameservermanagers.com/ requests?
* If sudo isn't installed, did you remove "sudo" from packages install commands?
* If `lib32gcc1 libstdc++6 libstdc++6:i386` packages won't install, did you run `apt update` after `dpkg --add-architecture i386`?
* If some dependencies are not available, did you check your /etc/apt/sources.list? (Debian based and apt only)

## Game server downloads

* Do you have enough disk space on the desired partition? Check command: `df -h`
* If the server requests a Steam login, did you enter it properly by editing your (example) "gameserver" script? It's a good idea to have a dedicated Steam account for that purpose.
* If the Steam download didn't work as intended, did you retry it, or try the [[validate]] command? Maybe your connection to Steam servers is faulty.
* Did you make sure that a firewall doesn't prevent the download from working? Check command: `iptables -L` ; See [[Firewalls]]

# Start issues

LinuxGSM servers are designed to work out of the box. However, if your server is unable to start, this can have multiple reasons. Some are user based, some are distro based. Here are some ways of diagnosing it.

Note: (example) `./gameserver details` will provide you with relevant information and save you some time. See [[details]]

## First start issues

* Is the server properly installed? See the "Game server downloads" part
* Are all packages installed properly? See "Dependencies" part
* Is your Linux installation compatible? 32/64bit, distribution... Check command: `uname -a`
* Are ports already used by another service? See [[Ports]] and [[Multiple Servers]]
* Is this a known tmux issue? See [[Tmux]]
* Did you try to start with the `debug` command? See [[debug]]
* What does the logs say? See [[Logging]]
* Do you have enough RAM? If not, do you have enough swap? Check command: `free -mh`
* Did you set an ip in your (example) gameserver script or config file?

## Modded servers start issues

* What does the logs say? See [[Logging]]
* Did you try to start with the `debug` command? See [[debug]]
* Did you wrongly append start parameters? See [[Start-Parameters]]
* Did you try temporarily removing mods, and adding them one by one?
* Does the user have the right permissions on its directories? If this is the case, a corresponding error should be displayed. See [[Permissions]]

## Server start issues after updates

* What does the logs say? See [[Logging]]
* Did you try to start with the `debug` command? See [[debug]]
* Did you try to validate your game files? (SteamCMD servers only) See [[validate]]
* Is a mod no longer compatible? Try temporarily removing mods, and adding them one by one.
* Is it an editor's error, breaking the server? Does it now require newer package versions? Check forums, alert us if needed by opening a Github issue (and check for existing ones).

# Connectivity issues

## Unable to connect or not showing up in server list

First off, you need to make sure that the server is started properly and listening.

### Is the server actually started?

*  Start it with (example `./gameserver start` , then check server logs (see [[Logging]]) to see if everything seems OK. You can also try the [[details]] command and [[monitor]] command to see if it's online and if it's able to answer simple queries. If not, then follow the "Start issues" section.

### Is the server actually listening?

`./gameserver details` will provide you with the corresponding command to check if the server process is properly listening.
Example sample output:
````
Useful port diagnostic command:
netstat -atunp | grep srcds_linux
````
Compare the output from this to expected ports displayed in the details command.

If this isn't enough, then here are some keys:

* Did you wait long enough? Sometimes it's just a matter of time until the server is fully started and listed into the master server list.
* What does the logs say? See [[Logging]]
* Did you set an ip in your (example) gameserver script or config file? Double check for typo mistakes.
* Are you listening to an actual interface IP? See [[Ports]]
* Are you behind [[Firewalls]]? See [[Firewalls]]
* If it's a local server, are ports redirection done properly? See [[Ports]] and [[details]]
* Are the ports you're using free? See [[Ports]]