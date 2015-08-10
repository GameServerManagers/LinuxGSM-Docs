A basic overview of how to use the server. For more advanced details on a feature see the feature page.

Configuration
==============
Config Files
------------
Most servers have a configuration file to alter the game server settings. This can be found by checking the server details.

````./csgoserver details````

````Config file:   /home/csgoserver/serverfiles/cstrike/cfg/csgo-server.cfg````

You can edit the config file with any linux text editor like nano or vi.

Start Parameters
------------
Servers commonly require start parameters that are command line options which are set with the servers executable when you start the server. These parameters can again be found in details. To alter them you will need to edit the main script file.

````vi csgoserver````

````./srcds_run -game fof -strictportbind -ip 192.168.1.1 -port 27015 +clientport 27005 +tv_port 27020 +map fof_depot +servercfgfile fof-server.cfg -maxplayers 16````

LGSM does not provide specific information about configuring your server. There are however many websites that provide documentation and support on configuring your server.

Running
=======

start
-----

    ./csgoserver start

stop
----

    ./csgoserver stop

restart
-------

    ./csgoserver restart

Updating
========

Most servers can be updated automatically using the update feature which uses SteamCMD.

update
------

Update checks with SteamCMD if any updates are available for the server. If there is update will stop a running server, apply the update and start it again.

    ./csgoserver update

validate
--------

You can use the validate option when updating the server.

    ./csgoserver validate

Automating Updates
------------------

You can use cronjobs to automate the process of updating the server. You can either run the cronjob as root or as the user.

### Root Cronjob

    crontab -e


    0 5 * * *  su – csgoserver -c '/home/csgoserver/csgoserver update-restart' > /dev/null 2>&1

### User Cronjob

    crontab -e


    0 5 * * *  /home/csgoserver/csgoserver update-restart > /dev/null 2>&1

Monitor
=======

Monitor will check the server to ensure it is online. Should the server go offline, the monitor will attempt to start it again and can report the issue via email. *Note: see gsquery.py for info on how monitor uses gsquery for improved monitoring.*

monitor
-------

    ./csgoserver monitor

### Email Notification

Monitoring can send you an email, should the server go offline, and report details of the issue. To enable ths feature do the following.

    nano csgoserver

    # Notification Email
    # (on|off)
    emailnotification="on"
    email="email@example.com"

email-test
----------

You can test the email feature using `email-test`

    ./csgoserver email-test

Automate Monitoring
-------------------

You can use cronjobs to automate the process of monitoring the server. You can either run the cronjob as root or as the user.

### Root Cronjob

    crontab -e


    0 5 * * *  su – csgoserver -c '/home/csgoserver/csgoserver monitor' > /dev/null 2>&1

### User Cronjob

    crontab -e


    0 5 * * *  /home/csgoserver/csgoserver monitor > /dev/null 2>&1

Debugging
========

debug
-----

Use debug mode to help you if you are having issues with the server. Debug allows you to see the output of the server directly to your terminal allowing you to diagnose any problems the server might be having.

    ./csgoserver debug

Logs
----

Server logs are available to monitor and diagnose your server. Script, console and game server (if available) logs are created for the server

    /home/csgoserver/logs

# Details


If you need to get all important server details you can use the following command.

    ./csgoserver details

# Console
console
-----

Console allows you to view the live console of a server as it is running and allow you to enter commands; if supported.

    ./csgoserver console

To exit the console press “CTRL+b d”.
> Note: pressing “CTRL+c” will terminate the server.

# Running on Boot
To run a server on boot add the command in to the rc.local file.

    nano /etc/rc.local
    su - csgoserver -c '/home/csgoserver/csgoserver start'