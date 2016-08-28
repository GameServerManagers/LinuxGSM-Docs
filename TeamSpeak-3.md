# General information

## Server Query

You can query your server to input commands without being connected to it through the TeamSpeak client.
To connect with Putty: Select telnet connection type and input your server query port (default is 10011).

#### Login
````
login serveradmin <password>
````

#### Generating a new Privilege key

````
use sid=<server-id>
tokenadd tokentype=0 tokenid1=6 tokenid2=0
````
Note : Your server ID is usually 1

### Reset your query password

Your query password is set and given to you upon the server installation. You'll also be able to find it into logs. However, if you lose it or wish to change it, we made a command to make it smoother.

````
./ts3server change-password
or
./ts3server pw
````

Your server will reboot and generate a new password.

## Database and MariaDB

TeamSpeak's database contains all user information, groups, and statistics from your server. 
By default, TeamSpeak uses an SQLIte database file, which allows good enough performance for most users, and easy server transfers from a machine to another.

However, you have the possibility to use MariaDB which is an alternative to MySQL to handle the database.
MariaDB is totally optionnal.
So during the install process, unless you need it, don't focus too hard on it, just discard the MariaDB message.

You'll find some clues on how to use it here https://www.digitalocean.com/community/questions/setup-teamspeak-server-ubuntu-15-04

## tsdns

Tsdns is a system allowing you to redirect a domain name to a given TeamSpeak port. Note that if you're using the default port, you don't need to provide the port when you're giving your server address, you can use the IP or domain name directly. Tsdns is handy only if you're hosting multiple TeamSpeak servers on a single machine.

You can display the documentation with
````
cat ~user/serverfiles/tsdns/tsdns_settings.ini.sample
````

You might find [additional information here](http://lastconnect.net/en/tsdnsdoc/).

Then you can copy the sample, edit it accordingly and restart your ts3server to apply the changes.
````
cd serverfiles/tsdns/
cp tsdns_settings.ini.sample tsdns_settings.ini
nano tsdns_settings.ini
cd ~
./ts3server restart
````

# Known issues

## IPv6

Some users with IPv6 enabled might encounter a server failing to start properly. The fix is to then edit your serverfiles/ts3-server.ini to add a standard IPv4 (voice_ip; filetransfer_ip; query_ip) and remove the ", ::" from IPv6. Then as the server failed to start at the installation, the privilege key hasn't been generated. So you'll need to use server query (ID/Password have been generated for them) to generate a new Server Admin privilege key.
