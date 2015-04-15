Backup will allow you to create a complete gzip archive of the whole server.

<pre>./csgoserver backup</pre>
This is designed to allow you to backup before making changes to the server in case of issues.

> Note: this is not designed to be an automated backup solution.

Example backup file created by backup.

    csgo-server-2015-01-23-155447.tar.gz

# Default Location

By default backups are saved in the ‘’backup’’ directory.

    ├── home</pre>
    ├── csgoserver 
        ├── backups **       
        ├── functions       
        ├── log       
        ├── serverfiles      
        ├── Steam       
        └── steamcmd

# Checking Backups

You can use [[details]] to get info on backups created.

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
    Backups:         6.2G</pre>