### Database and MariaDB

TeamSpeak's database contains all user information, groups, and statistics from your server. 
By default, TeamSpeak uses an SQLIte database file, which allows good enough performance for most users, and easy server transfers from a machine to another.

However, you have the possibility to use MariaDB which is an alternative to MySQL to handle the database.
MariaDB is totally optionnal.
So during the install process, unless you need it, don't focus too hard on it, just discard the MariaDB message.

You'll find some clues on how to use it here https://www.digitalocean.com/community/questions/setup-teamspeak-server-ubuntu-15-04


## Known issues

### IPv6

Some users with IPv6 enabled might encounter a server failing to start properly. The fix is to then edit your serverfiles/ts3-server.ini to add a standard IPv4 (voice_ip; filetransfer_ip; query_ip) and remove the ", ::" from IPv6. Then as the server failed to start at the installation, the privilege key hasn't been generated. So you'll need to use server query (ID/Password have been generated for them) to generate a new Server Admin privilege key.

With putty : Use telnet type, default port is 

````
login serveradmin <password>
use sid=<server ID>
tokenadd tokentype=0 tokenid1=6 tokenid2=0
````
