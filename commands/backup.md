# backup

The `backup` command allows the creation of `.tar.gz` archives of a game server. This can be used to transfer a game server to another Linux server, to backup the game server before a risky change, to save the current state of the game server.

{% hint style="danger" %}
Each time a backup runs the whole game server will be backed up, this can take up significant storage space. Consider a backup policy to prevent your Linux server from running out of storage.
{% endhint %}

## Commands

Standard: `./gameserver backup`

Short: `./gameserver b`

## Example Output

```text
mumbleserver@game:~$ ./mumbleserver b
[ INFO ] Backup mumble-server: A total of 34M will be compressed into the following backup:
/home/mumbleserver/backups/mumble-server-2016-10-28-194346.tar.gz
Warning! mumble-server will be stopped during the backup.
[  OK  ] Stopping mumble-server: Mumble Port 64738
[  OK  ] Backup mumble-server: Backup created: mumble-server-2016-10-28-194346.tar.gz is 36M size
```

## Backup Settings

Alter these three settings by editing [LinuxGSM config](../configuration/linuxgsm-config.md).

### maxbackups

Set the maximum number of backups with `maxbackups`. If the number of backups exceeds this value, the oldest backup will be removed after a successful backup.

```bash
maxbackups="4"
```

{% hint style="info" %}
Setting the value to 0 will prevent any backups from being saved, including the one just created.
{% endhint %}

### maxbackupdays

Set the maximum age of a backup using `maxbackupdays`. Any backups older than X days will be removed after a successful backup.

```bash
maxbackupdays="30"
```

{% hint style="info" %}
Setting the value to 0 will retain the backup for 24 hours.
{% endhint %}

### stoponbackup

Set if the server should be stopped for a backup using `stoponbackup`. If the server is running it will be stopped while the backup is running and started again once complete. This is useful to prevent any file changes during compression that could result in a corrupt or failed backup.

```bash
stoponbackup="on"
```

## Automated Backups

Automated backups can be set using [cronjobs](../configuration/cronjobs.md). It is recommended that frequently you backup and your retention policy to prevent your server is carefully considered to prevent storage issues.

### cronjob example

see [cronjobs](../configuration/cronjobs.md)

```bash
crontab -e
```

```bash
0 5 * * *  /home/username/gameserver backup > /dev/null 2>&1
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

Use `./gameserver details` to view information about created backups.

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

## Alternative Backup Methods

Using the backup feature is not the only way to backup a game server. There are other methods that have more features are are more powerful than the basic LinuxGSM backup feature. Below are are few applications that can be used instead of, or with LinuxGSM backups.

### rsync

[rsync](https://www.linode.com/docs/tools-reference/tools/introduction-to-rsync) is one of the most common ways to backup. It is a remote sync tool that is created for sending files/directory's to another location. Particularly good for syncing to another server.

{% embed url="https://www.linode.com/docs/tools-reference/tools/introduction-to-rsync" caption="" %}

### Duplicity

Is an incremental backup solution that allows backups to all sorts of different locations including many different cloud storage solutions like BackBlaze B2 and Amazon S3. Once configured it can be a powerful and efficient backup solution.

{% embed url="http://duplicity.nongnu.org" caption="" %}

#### duplicity-backup.sh

duplicity-backup.sh is a very useful bash wrapper to help automate duplicity.

{% embed url="https://github.com/zertrin/duplicity-backup.sh" caption="" %}

### rclone

[rclone](http://rclone.org) is similar to rsync however can easily sync to cloud storage solutions.

{% embed url="http://rclone.org" caption="" %}

