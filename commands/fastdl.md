# fastdl

FastDL \(Fast Download\) allows the client to download custom server content \(maps, materials, models, particles, sounds, fonts, images\) from a web server.

It is used to offload content downloads to a web server instead of relying on source servers \(SRCDS\) that only allows 20KBps downloads to clients. Content on the web server can be compressed to further speed up the download process. This means that custom content downloads much faster.

Valve now use steam workshop for most custom content however FastDL is still required in some cases.

LinuxGSM FastDL automatically creates the web directories and compresses the content for you.

## Supported Servers

* All Source engine servers

## Commands

Standard: .`/gameserver fastdl`

Short: `./gameserver fd`

## Supported file formats

* Maps \(.bsp\)
* Materials \(.vtf, .vmt\)
* Models \(.vtx, .vvd, .mdl, .phy\)
* Particles \(.pcf\)
* Sounds \(.wav, .mp3, .ogg\)
* Fonts \(.otf, .ttf\)
* Images \(.png, .svg\)

## Requirements

* Web server on the game server \(Apache/Nginx\).

  or

* Access to a remote web server.

## Usage

### Generate Compressed files

Run the FastDL command on your main LinuxGSM script. This will create a new directory `/home/gameserver/public_html/fastdl`

`./gameserver fastdl`

### Create A virtual Host \(local Apache web server\)

If Apache2 is being used a virtual host pointing to the newly created `public_html` directory can be used.

Tip: Apache2 mod "userdir" is useful if the Linux server is hosting [multiple game servers](../features/multiple-game-servers.md), as it creates a url for the current user `http://yourwebsite.ltd/~username`.

#### Tutorial on setup of Apache2 server with Virtual Hosts

Here is an example of setting up Apache2 using a subdomain.

This works for Apache 2.4+ and when using a domain name. If you have got a different configuration, refer to the Apache2 documentation.

Firstly make sure your subdomain redirects to your game server and that Apache2 is correctly installed and started. Create a virtual host in order to be able to host a website :

`nano /etc/apache2/sites-available/yourvirtualhost.com.conf`

See the example below and edit the relevent details.

```text
<VirtualHost *:80>
        ServerAdmin adminemail@domain.com
        ServerName subdomain.domain.com
        ServerAlias subdomain.domain.com
        DocumentRoot /home/gameserver/public_html
        <Directory /home/gameserver/public_html>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride All
                Require all granted
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/error.log
        # Possible values include: debug, info, notice, warn, error, crit, alert, emerg.
        LogLevel warn
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Enable your website by restarting Apache2

```text
a2ensite yourvirtualhost.com.conf
service apache2 reload
```

Test the domain, to make sure it is working `http://subdomain.domain.com/fastdl`

### Edit Game Server config

The new url will need to be added to the [game server config](../configuration/game-server-config.md)

`nano serverfiles/gamename/cfg/game-server.cfg`

Make sure you have this:

```text
sv_downloadurl "http://subdomain.domain.com/fastdl"
sv_allowdownload 1
```

### Re-generate FastDL

If the custom server content is updated or removed re running the fastdl command is required to ensure that the webserver is in sync with the game server.

> Note for addons developers : Note that clients won't download a file that they already downloaded unless you rename it.

### Bzip2 Compression

Custom server content can be compressed using bzip2 which is supported by source games, allowing clients downloads will be faster. It is a must-have if you're hosting large files, as it will save you bandwidth, and speed up downloads for clients. However, using bzip2 on many small files can slow down client loading times.

#### Garry's Mod Download enforcer

In order for a client to download files from a FastDL in Garry's Mod, the developer of an addon must put files from the addon into lua code `resource.Addfile ( "/path/to/file.ext" )`. However, some addon developers do not do this. In order for clients to download the required files, an lua file needs to be generated for it to work, which is what the lua enforcer feature does. The only downside is that clients may download files that are not required on the server.

