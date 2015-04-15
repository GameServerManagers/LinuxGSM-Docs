It is possible to run multiple server instances. There are a couple of methods depending on how you want to configure your server.

Separate Installation (Easy)
============================
Repeat the installation process with a different username and change the ports within the script.

directory:

    /home/csgoserver
    /home/csgoserver2

Same Installation Different Config File (Advanced)
==================================================
directory:

    /home/csgoserver

script:

    ./csgoserver
    ./csgoserver2

 cfg directory:

     csgo-server.cfg
     csgo-server2.cfg

Copy and rename the script.

    cp csgoserver csgoserver2

Edit csgoserver2.

    nano csgoserver2

Rename the servicename variable.

    servicename="csgo-server2"

Change the server ports.

    serverport=2302
    steamport=2304;
    steamqueryport=2303;

Copy and rename the server config file.

    cp csgo-server.cfg csgo-server2.cfg

Alter the new configuration file to suite your needs.