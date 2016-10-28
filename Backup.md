The backup command will allow you to create .tar.gz archives of a gameserver. This can be used to transfer a server to another physical machine, to save your work before a risky change, to save the current state of the server and any many more.

**Commands**: 

````bash
./gameserver backup
./gameserver b
````

Example output:

```
mumbleserver@game:~$ ./mumbleserver b
[ INFO ] Backup mumble-server: A total of 34M will be compressed into the following backup:
/home/mumbleserver/backups/mumble-server-2016-10-28-194346.tar.gz
Warning! mumble-server will be stopped during the backup.
[  OK  ] Stopping mumble-server: Mumble Port 64738
[  OK  ] Backup mumble-server: Backup created: mumble-server-2016-10-28-194346.tar.gz is 36M size
```

# Backup settings

You can alter three settings by editing your `gameserver `file.

1. How many backups to keep. If the amount of backups exceeds this value, then the oldest backups will be removed after a successful backup.

````bash
maxbackups="4" 
````
Note: A value of 0 will mean don't keep any backup, even the one you just created.

2. How long a backup should last. Older than `x` days backups will get removed upon successful backup.

````bash
maxbackupdays="30"
````

Note: A value of 0 stands for 24h.

3. If the game server is started, then stop it before running the backup and restart it afterwards. This is useful to prevent any file change during compression that would result in a failure. 

````bash
stoponbackup="on" # on/off
````

# Automated backups

You can now set automated backups using [cronjobs](https://github.com/GameServerManagers/LinuxGSM/wiki/Cronjobs). However, you should make sure that your backup settings and the cronjob frequency are set according to the size of the gameserver you want to backup and to your disk space.

## Root cronjob example

````bash
crontab -e

0 5 * * *  su - username -c '/home/username/gameserver backup' > /dev/null 2>&1
````

# Backups Location

By default backups are saved in the backup directory.

    ├── home
    ├── csgoserver 
        ├── ** backups **       
        ├── lgsm
        ├── log       
        ├── serverfiles      


# Checking Backups

You can use /.gameserver [[details]] to get info about created backups. Example : 

    Backups
    ===============================================================================
    No. of backups:    1
    Latest backup:
        date:          Fri Jan 23 15:54:52 CET 2015
        file:          /home/csgoserver/backups/csgo-server-2015-01-23-155447.tar.gz
        size:          1.6G
    
    Disk Usage
    ===============================================================================
    Disk available:  5.4G
    Serverfiles:     1.6G
    Backups:         6.2G