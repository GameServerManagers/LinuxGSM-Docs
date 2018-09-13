# TeamSpeak 3

## Connect to TeamSpeak 3 Server

You can connect to a TeamSpeak 3 server to input commands without the need for a TeamSpeak 3 client. This can be done by connecting to the query port using telnet.

Using PuTTY or equivalent select a telnet connection and enter the server IP and TeamSpeak 3 query port \(default:10011\).

### Useful Commands

#### Login

```text
login serveradmin <password>
```

#### Generating a new Privilege key

```text
use sid=<server-id>
tokenadd tokentype=0 tokenid1=6 tokenid2=0
```

> Note: Your server ID is usually 1

#### Reset your query password

See [change password](../commands/change-password.md).

## TeamSpeak 3 Databases

The TeamSpeak 3 database contains all user information, groups, and statistics for your server.

### SQLite Database

By default, TeamSpeak 3 uses an SQLite database file, which allows good performance for most users, and easy server transfers from one server to another. This method is recommended for most admins as it is the simplest database method to use.

### MariaDB

TeamSpeak 3 also allows admins to use MariaDB \(MySQL alternative\) manage the database. MariaDB is entirely optional and is not required so it is recommended that admins only use if they are comfortable.

Information about installing TeamSpeak 3 with MariaDB can be found [here](https://www.digitalocean.com/community/questions/setup-teamspeak-server-ubuntu-15-04).

### TSDNS

TSDNS is a system allowing admins to redirect a domain name to a given TeamSpeak 3 port.

If TeamSpeak 3 port is using the default port, you do not need to provide the port when you are giving your server address, you can use the IP or domain name directly.

TSDNS is useful to admins that are hosting multiple TeamSpeak 3 servers on a single dedicated server.

Further documentation can be found using the following command.

```text
cat ~user/serverfiles/tsdns/tsdns_settings.ini.sample
```

Additional information can be found [here](http://lastconnect.net/en/tsdnsdoc/).

Then you can copy the sample, edit it accordingly and restart your TeamSpeak 3 server to apply the changes.

```text
cd serverfiles/tsdns/
cp tsdns_settings.ini.sample tsdns_settings.ini
nano tsdns_settings.ini
cd ~
./ts3server restart
```

## Known issues

### IPv6

Some users with IPv6 enabled might encounter a server failing to start properly. To fix this edit `serverfiles/ts3-server.ini` to add a standard IPv4 \(`voice_ip; filetransfer_ip; query_ip`\) and remove the `, ::` from IPv6. Then as the server failed to start at the installation, the privilege key hasn't been generated. So you will need to use server query \(ID/Password have been generated for them\) to generate a new Server Admin privilege key.

