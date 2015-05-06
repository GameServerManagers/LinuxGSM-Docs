A basic overview of how to use the server. For more advanced details on a feature see the feature page.

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

This will also restart the server if it is currently online.

    ./csgoserver update

validate
--------

You can use the validate option when updating the server.

    ./csgoserver validate

validate-restart
----------------

`validate-restart` will stop the server run validate and start the server.

    ./csgoserver validate-restart

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


Console allows you to view the live console of a server as it is running and allow you to enter commands; if supported.

    ./arma3server console

To exit the console press “CTRL+b d”.
> Note: pressing “CTRL+c” will terminate the server.

# Running on Boot
To run arma3server on boot add the command in to the rc.local file.

    nano /etc/rc.local
    su - arma3server -c '/home/arma3server/arma3server start'