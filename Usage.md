Get your script and basic instructions [here](http://gameservermanagers.com/). Don't forget to install required packages.
***

# General Usage

A basic overview of how to use LGSM. For more advanced details on a feature see the feature page.

**Note** : Replace generic "gameserver", "gamename", and "username" from these examples by your actual script, game, and user names.

Configuration
==============
Config Files
------------
Most servers have a configuration file to alter the game server settings. This can be found by checking the server details. This command will also provide you several useful information about your game server and your machine.

````./gameserver details````

````Config file:   /home/username/serverfiles/gamename/cfg/gamename-server.cfg````

You can edit the config file with any linux text editor like nano or vi.

Start Parameters
------------
You probably want to change some of them. Servers commonly require start parameters that are command line options which are set with the servers executable when you start the server. These parameters can again be found in details. To alter them, you will need to edit the main script file.

````vi gameserver````

or 

````nano gameserver````

You will find most important variables such as : 

    # Start Variables
    defaultmap="map_name"
    gamemode="game_mode"
    maxplayers="42"
    port="27015"
    sourcetvport="27020"
    clientport="27005"
    ip="0.0.0.0"
    updateonstart="off"

You may also configure the [GSLT](Game-Server-Login-Token) for some servers (required for CSGO, optional for others).

LGSM does not provide specific information about configuring your server. There are however many websites that provide documentation and support on configuring your server. If you wish to add more start parameters, see [[Start-Parms]].

Running
=======

start
-----

    ./gameserver start

stop
----

    ./gameserver stop

restart
-------

    ./gameserver restart

Updating
========

Most servers can be updated automatically using the update feature which uses SteamCMD.

update
------

[[Update]] checks with SteamCMD if any updates are available for the server. The server will update and restart only if required.

    ./gameserver update

validate
--------
You can use the [validate](https://github.com/dgibbs64/linuxgsm/wiki/Update#when-an-update-isnt-enough) option when updating the server.

    ./gameserver validate

Automating Updates
------------------

You can use cronjobs to automate the process of updating the server. We advise to use root cronjobs for convenience when running multiple servers, but you can run user cronjobs as well. See [[Automation]].

### Root Cronjob

    crontab -e


    0 5 * * *  su - username -c '/home/username/gameserver update' > /dev/null 2>&1

### User Cronjob

    crontab -e


    0 5 * * *  /home/username/gameserver update > /dev/null 2>&1

Monitor
=======

[[Monitor]] will check the server to ensure it is online. Should the server go offline, the monitor will attempt to start it again and can report the issue via email. The whole point to this function is to be [automated with cronjobs](https://github.com/dgibbs64/linuxgsm/wiki/Automation). *Note: see gsquery.py for info on how monitor uses gsquery for improved monitoring.*

monitor
-------

    ./csgoserver monitor

### Email Notification

Monitoring can [send you an email](https://github.com/dgibbs64/linuxgsm/wiki/Monitor#email-notifications), should the server go offline, and report details of the issue. To enable ths feature do the following.

    nano csgoserver

    # Notification Email
    # (on|off)
    emailnotification="on"
    email="email@example.com"

email-test
----------

You can test the email feature using `email-test`

    ./gameserver email-test

Automate Monitoring
-------------------

You can use cronjobs to automate the process of monitoring the server. You can either run the cronjob as root or as the user.

### Root Cronjob

    crontab -e


    */5 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1

### User Cronjob

    crontab -e


    */5 * * * *  /home/username/gameserver monitor > /dev/null 2>&1

Debugging
========

debug
-----

Use debug mode to help you if you are having issues with the server. Debug allows you to see the output of the server directly to your terminal allowing you to diagnose any problems the server might be having.

    ./gameserver debug

Logs
----

Server logs are available to monitor and diagnose your server. Script, console and game server (if available) logs are created for the server

    /home/username/logs

# Details


If you need to get all important server details you can use the following command.

    ./gameserver details

# Console
console
-----

Console allows you to view the live console of a server as it is running and allow you to enter commands; if supported.

    ./gameserver console

To exit the console press “CTRL+b, then d”.
> Note: pressing “CTRL+c” will terminate the server.

# Running on Boot
To run a server on boot, either use the monitor cronjob that will restart any server that was online before a reboot (advised, see [[Monitor#automated-monitoring]] ), or add a command in to the rc.local file that works with most distro : 

    nano /etc/rc.local
    su - username -c '/home/username/gameserver start'

# Updating your LGSM script
LGSM has the ability to self update functions.

update-functions
-----

    ./gameserver update-functions