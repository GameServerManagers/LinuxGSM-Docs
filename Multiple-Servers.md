It is possible to run multiple server instances. There are a couple of methods depending on how you want to configure your server.

Separate Installation (Easy)
============================
Repeat the installation process with a different username and change the [[Default-Ports]] within the script.

directory:

    /home/username1
    /home/username2

Same Installation Different Config File (Advanced)
==================================================
**Important note** : Database file (sv.db) and any other data file (such as garrysmod/data folder) will be shared by those servers, which can either be an advantage or an issue.

directory:

    /home/username

script:

    ./gameserver1
    ./gameserver2

 cfg directory:

     csgo-server.cfg
     csgo-server2.cfg

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

Copy and rename the server config file.

    cd serverfiles/gamename/cfg
    cp game-server.cfg game-server2.cfg

Alter the new configuration file to suite your needs.