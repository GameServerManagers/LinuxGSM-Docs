# backup

The `backup` command will allow you to create .tar.gz archives of a gameserver. This can be used to transfer a server to another physical machine, to save your work before a risky change, to save the current state of the server and any many more.

> Note: Each time a backup runs the whole game server will be backed up, this can take up significant storage space. Consider a backup policy to prevent your server from running out of disk space.

## Commands

Standard: `./gameserver backup`

Short: `./gameserver b`

### Example output

```text
mumbleserver@game:~$ ./mumbleserver b
[ INFO ] Backup mumble-server: A total of 34M will be compressed into the following backup:
/home/mumbleserver/backups/mumble-server-2016-10-28-194346.tar.gz
Warning! mumble-server will be stopped during the backup.
[  OK  ] Stopping mumble-server: Mumble Port 64738
[  OK  ] Backup mumble-server: Backup created: mumble-server-2016-10-28-194346.tar.gz is 36M size
```

## Backup settings

You can alter three settings by editing your `gameserver`file.

### maxbackups

Set the maximum backups you want to keep with `maxbackups`. If the number of backups exceeds this value, then the oldest backup will be removed after a successful backup.

```bash
maxbackups="4"
```

> Note: Setting the value to 0 will prevent any backups from being saved, including the one you just created.

### maxbackupdays

Set the maximum age of a backup using `maxbackupdays`. Any backups than X days will be removed after a successful backup.

```bash
maxbackupdays="30"
```

> Note: Setting the value to 0 will retain the backup for 24 hours.

### stoponbackup

Set if the server should be stopped for a backup using `stoponbackup`. If the server is running it will be stopped while the backup is running and started again once complete. This is useful to prevent any file changes during compression that could result in a corrupt or failed backup.

```bash
stoponbackup="on"
```

## Automated backups

You can setup automated backups using [cronjobs](https://github.com/GameServerManagers/LinuxGSM/wiki/Cronjobs). It is recommended that you carefully consider how frequently you backup and your retention policy to prevent your server from running out of space.

### Root cronjob example

```bash
crontab -e

0 5 * * *  su - username -c '/home/username/gameserver backup' > /dev/null 2>&1
```

## Backups Location

By default backups are saved in the `backup` directory.

```text
├── home
├── csgoserver 
    ├── ** backups **       
    ├── lgsm
    ├── log       
    ├── serverfiles      
```

## Checking Backups

You can use ./gameserver \[\[details\]\] to get information about created backups.

```text
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
```

## Alternative backup Methods

Using the backup feature is not the only way to backup your server. There are other methods that have more features are are more powerful than the basic LinuxGSM backup feature. Below are are few applications that you can use instead of or with the LinuxGSM backup and are great tools for Linux command line backups.

### rsync

rsync is one of the most common ways to backup. It is a remote sync tool that is create for sending files/directory's to another location. Particularly good for syncing to another server.

[https://www.digitalocean.com/community/tutorials/how-to-use-rsync-to-sync-local-and-remote-directories-on-a-vps](https://www.digitalocean.com/community/tutorials/how-to-use-rsync-to-sync-local-and-remote-directories-on-a-vps)

### Duplicity

Is an incremental backup solution that allows to you backup to all sorts of different locations including many different Cloud storage solutions like BackBlaze B2 and Amazon S3. Once configured it can be a powerful and efficient backup solution. [http://duplicity.nongnu.org/](http://duplicity.nongnu.org/)

#### duplicity-backup.sh

duplicity-backup.sh is a very useful bash wrapper to help automate duplicity. [https://github.com/zertrin/duplicity-backup.sh](https://github.com/zertrin/duplicity-backup.sh)

### rclone

Similar to rsync however you can easily sync to cloud storage solutions.

[http://rclone.org/](http://rclone.org/)

