FastDl script is now available for Garry's Mod only, but will be deployed for other source games as well.


## What is FastDL ?

FastDL for "fast download" is used for the client to download custom server content (maps, materials, models, particles, sounds, fonts, images). It's used as a workaround for Source (SRCDS) servers natively uploading at only 20KB/s to clients. It basically consists in sharing the required files with an HTTP server, that will allow clients to download those files much faster. But as the making of that shared folder is a pain to make manually, we developed a script to make it automatically.

## Requirements

* HTTP server onto the game server (easiest)

OR 

* FTP + HTTP server on a remote server


## Supported games : 

Source engine games like TF2, HL2DM, CSS, CSGO, Garry's Mod (with more advanced features required).

## Usage

#### 1) Run the FastDL command on your main LGSM script : 

`./gameserver fastdl` or the short version `./gameserver fd`

If you're using an older LGSM installation, run `./gameserver update-function`s or `./gameserver uf` to get the new FastDL feature.

This will create a new folder in your game server's directory : public_html/fastdl

That way, you can make another folder into the public_htmlfolder if you need to, like public_html/loadingurl

#### 2) Share FastDL content with an HTTP server

If you're used to Apache2 and running websites , then that step is pretty straight forward : 

**a)** Make a new virtual host pointing to /home/youruser/public_html, using a domain or subdomain

Note : Apache2's mod "userdir" is a clever way if your server will run many game servers. Make it so that every "www" folder from every user has its website, which will be accessible with an address like http://yourwebsite.ltd/~username

**b)** Go to step 3


#### Help 
> "I'm no web admin !! HOWDOIDO ?!"

Here is an example using a subdomain. 

**This works for Apache 2.4+ and when using a domain name. If you've got a different configuration, please, refer to Apache2's documentation. Remember to not be a dumbass and use google wisely before crying on github.**
If you don't own a domain, then you should really consider getting one, it starts for a few bucks per year.

Before anything, make sure your subdomain redirects to your game server and that Apache2 is correctly installed and started.
First, create a virtual host in order to be able to host a website : 

`nano /etc/apache2/sites-available/yourvirtualhost.com.conf`


Edit everything between brackets {} (and remove the brackets) and paste this : 

````
<VirtualHost *:80>
        ServerAdmin {adminemail@mail.com}
        ServerName {subdomain.domain.com}
        ServerAlias {subdomain.domain.com}
        DocumentRoot /home/{youruser}/www
        <Directory /home/{youruser}/www>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride All
                Require all granted
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/error.log
        # Possible values include: debug, info, notice, warn, error, crit, alert, emerg.
        LogLevel warn
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
````

Then enable your website and restart apache2

````
a2ensite yourvirtualhost.com.conf
service apache2 reload
````

Test your address, you be able to access files with a link like that : 

http://subdomain.domain.com/fastdl

#### 3) Edit your game config to use the FastDL Link

`nano serverfiles/gamename/cfg/game-server.cfg`

Make sure you have this : 

````
sv_downloadurl "http://subdomain.domain.com/fastdl"
sv_allowdownload 0
````

`sv_allowdownload 0` disables client downloading using SRCDS which is slow, and which you want to do using FastDL.



## Features and settings

### Clear old FastDL files

It's required to clear the old FastDL folder in 2 cases : 

1) If you want to clean files that are no longer into the server content

2) If some files changed and you're using bzip2 compression.

Important note for addons developers : Note that clients won't download a file that they already downloaded unless you rename it.

### bzip2 compression

You can compress your files using bzip2 which is supported by source games. That way, clients downloads will be faster. It's a must-have if you're hosting big files, will save you some bandwidth, and will make downloads faster for your clients. Howerver, slow client's machine may be slowed down a bit if you're using it for small files only.

### Supported file formats

* Maps (.bsp)
* Materials (.vtf, .vmt)
* Models (.vtx, .vvd, .mdl, .phy)
* Particles (.pcf)
* Sounds (.wav, .mp3, .ogg)
* Fonts (.otf, .ttf)
* Images (.png)

### Garry's Mod special features

#### Download enforcer
In order for a client to download files from a FastDL in Garry's Mod, the developer of an addon must put "resource.Addfile ( "/path/to/file.ext" ) for every file from his addon into its lua code. Some of them don't bother with that. So in order for clients to download the required files, it is then needed to generate a lua file for that to work, and this is what the lua enforcer feature does. The only possible downside is that clients may download non required files as well. 