## Two good ways of making multiple servers

Running several servers is pretty easy as long as you follow this guide. There is a couple ways to do it.

* The first method is basically: Make a new user, repeat the install process, configure the server to use different ports, enjoy. It's the best and easiest way to do. It will use more disk space, but will avoid several problems by making these servers totally independent.

* The second is basically: Re-use an already existing server and make a new instance of it (of course with different ports). This is a bit more painful, a bit less reliable, and of course, those servers will share addons, databases and so on. The only thing you'll be able to customize from one server to another will eventually be the main config file, gamemode, and anything that you can configure in your "gameserver" script.

* The third is for jerks that wish to run several independent servers within the same user. See how "independent" and "same user" don't match together ? LGSM hasn't been designed in that philosophy, but you can manage to do it.


## Separate Installations (Advised)

Basically > Repeat the installation process with a different username and change the [[Default-Ports]] within the script.

Here is an example of how you can do it.

1. Login to root

2. Create a new user: `adduser mynewuser`

3. Login to it: `login mynewuser`

4. Get your game script at http://gameservermanagers.com/

5. Edit and configure your script to make sure your game server is using its own ports: `nano mygameserver` (For more information on how to configure ports, see [[Default-Ports]])

6. Install , and enjoy. 


## Same Installation Different Config File

**Important note**: Database file (sv.db) and any other data (such as garrysmod/data or /csgo/addons folders) will be shared by those servers, which can either be an advantage or an issue, but will most of the time be an issue. You cannot say we didn't tell you.

**What you're gonna end up with**

One directory:

    /home/username

Two scripts:

    ./gameserver1
    ./gameserver2

Two config files in serverfiles/gamename/cfg: 
 
     csgo-server.cfg
     csgo-server2.cfg


**How to do**
Copy and rename the script.

    cp gameserver gameserver2

Edit gameserver2.

    nano gameserver2

Rename the servicename variable.

    servicename="game-server2"

Change the server ports. See [[Default-Ports]]

    serverport="27115"
    steamport="27150"
    steamqueryport="27100"

Copy and rename the server config file to fit the 2nd servicename.

    cd serverfiles/gamename/cfg
    cp game-server.cfg game-server2.cfg

Alter the new configuration file to suite your needs.

## Same user, several installation folders

If you're a jerk, and wish to install several servers within the same user... You can. However, it's not advised. You're probably gonna have to change the [[Default-Ports]], especially if those games are running the same engine. If you wish to run two servers for the same game, you're gonna have to change the servicename and config file names, just like for the previous method.

**What you're gonna end up with**
Two directories:

    /home/username/server1
    /home/username/server2

Two scripts:

    /home/username/server1/gameserver
    /home/username/server2/gameserver

**How to do**
Make sure that each server has its own folder.

    /home/username/server1
    /home/username/server2

Go through the [[Installer]] process, being in each folder.

Edit your second server.

    nano /home/username/server2/gameserver

Rename the servicename variable.

    servicename="game-server2"

Change the server ports. See [[Default-Ports]]

    serverport="27115"
    steamport="27150"
    steamqueryport="27100"

Rename the server config file to fit the 2nd servicename.

    cd /home/username/server2/serverfiles/gamename/cfg
    mv game-server.cfg game-server2.cfg