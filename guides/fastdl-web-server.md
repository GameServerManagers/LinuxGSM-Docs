---
description: Serve LinuxGSM FastDL files with nginx or Apache, in Docker or installed on the server.
---

# FastDL Web Server

The [fastdl](../commands/fastdl.md) command prepares the files, but players download them from a web server. This guide shows the quickest ways to serve them and point the game server at them.

Any web server that can serve static files over HTTP will work. Pick one option:

| Option | Best for |
| --- | --- |
| [nginx in Docker](#option-1-nginx-in-docker) | The quickest setup if Docker is installed. Nothing else to install or configure. |
| [nginx on the server](#option-2-nginx-on-the-server) | Servers without Docker. |
| [Apache on the server](#option-3-apache-on-the-server) | Servers already running Apache. |
| [An existing web host](#option-4-an-existing-web-host) | Serving from a web host or another machine. |

## Before you start

* **Generate the files first.** Run `./gameserver fastdl`. By default the files are created in `public_html/fastdl` inside the LinuxGSM installation directory, for example `/home/gameserver/public_html/fastdl`. The examples below use that path and the user `gameserver`. Change them to match your server.
* **Pick a port.** The examples use port `8080` so they do not clash with a website already on port `80`. Allow the port through your firewall and any cloud provider firewall. See [Ports](../networking/ports.md) if you need help.
* **Know your address.** Players need to reach the web server from the internet, so use the server's public IP address or a domain name pointing at it. The examples use `203.0.113.10`.

When a player joins, the game asks the web server for each file it is missing at `<sv_downloadurl>/<path>`. Source games ask for the compressed `.bz2` file first, for example `http://203.0.113.10:8080/fastdl/maps/koth_example.bsp.bz2`, and fall back to the uncompressed file if it is not found. The web server only needs to serve files: no PHP, database or directory listing is needed.

## Option 1: nginx in Docker

This runs the official nginx image and shares `public_html` with it read-only. Docker reads the files directly, so the home folder permission problems covered in [Troubleshooting](#troubleshooting) do not apply.

```bash
docker run -d \
  --name fastdl \
  --restart unless-stopped \
  -p 8080:80 \
  -v /home/gameserver/public_html:/usr/share/nginx/html:ro \
  nginx:stable
```

Or, with Docker Compose, save this as `compose.yaml` and run `docker compose up -d`:

```yaml
services:
  fastdl:
    image: nginx:stable
    container_name: fastdl
    restart: unless-stopped
    ports:
      - "8080:80"
    volumes:
      - /home/gameserver/public_html:/usr/share/nginx/html:ro
```

New and changed files appear as soon as `fastdl` writes them, so the container never needs restarting.

{% hint style="info" %}
To use Apache instead, use the `httpd:2.4` image and mount the folder at `/usr/local/apache2/htdocs` instead. Apache shows a list of the files when a folder is opened in a browser, which is harmless because the files are public anyway.
{% endhint %}

{% hint style="warning" %}
Ports published by Docker are opened in the server's firewall directly, so they bypass `ufw` rules. Use your cloud provider's firewall if you need to restrict access.
{% endhint %}

Then [point the game server at it](#point-the-game-server-at-the-web-server) using `http://203.0.113.10:8080/fastdl`.

## Option 2: nginx on the server

Install nginx:

```bash
sudo apt install nginx
```

Create `/etc/nginx/sites-available/fastdl` with the following. It serves only the `fastdl` folder and returns "not found" for everything else.

```nginx
server {
    listen 8080;
    listen [::]:8080;
    server_name _;

    root /home/gameserver/public_html;

    location /fastdl/ {
        autoindex off;
    }

    location / {
        return 404;
    }
}
```

Give nginx permission to read the files, then enable the site and reload nginx:

```bash
sudo usermod -aG gameserver www-data
sudo ln -s /etc/nginx/sites-available/fastdl /etc/nginx/sites-enabled/fastdl
sudo nginx -t
sudo systemctl reload nginx
```

The `usermod` line adds the web server user to the `gameserver` group. Ubuntu 21.04 and later make home folders private to their owner and group, and without this nginx returns `403 Forbidden`.

Then [point the game server at it](#point-the-game-server-at-the-web-server) using `http://203.0.113.10:8080/fastdl`.

## Option 3: Apache on the server

Install Apache:

```bash
sudo apt install apache2
```

Create `/etc/apache2/sites-available/fastdl.conf`:

```apacheconf
Listen 8080
<VirtualHost *:8080>
    DocumentRoot /home/gameserver/public_html
    <Directory /home/gameserver/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>
</VirtualHost>
```

Give Apache permission to read the files, then enable the site and reload Apache:

```bash
sudo usermod -aG gameserver www-data
sudo a2ensite fastdl
sudo apache2ctl configtest
sudo systemctl reload apache2
```

To serve FastDL from an existing website instead, add the `<Directory>` block to that site and change `DocumentRoot`, or set [`webdir`](../commands/fastdl.md#web-directory) to a folder inside that site.

If players request files with different upper and lower case to the files on the server, see [Make Webserver Case Insensitive](make-webserver-case-insensitive.md).

Then [point the game server at it](#point-the-game-server-at-the-web-server) using `http://203.0.113.10:8080/fastdl`.

## Option 4: An existing web host

Any web host that serves static files will do. Copy the `fastdl` folder to it after each `fastdl` run, for example with `rsync`:

```bash
rsync -av /home/gameserver/public_html/fastdl/ user@webhost.example.com:/var/www/html/fastdl/
```

Only add `--delete` to the command if the folder on the web host holds nothing but FastDL files, because it deletes everything there that is not in your local `fastdl` folder.

Then [point the game server at it](#point-the-game-server-at-the-web-server) using the web host's address, for example `http://webhost.example.com/fastdl`.

## Point the game server at the web server

Add these lines to the [game server config](../configuration/game-server-config.md), for example `serverfiles/tf/cfg/tf2server.cfg`, and restart the game server:

```
sv_downloadurl "http://203.0.113.10:8080/fastdl"
sv_allowdownload 1
```

* Use the address of the `fastdl` folder itself, not `public_html`.
* `http://` works with every game. Current Source games also accept `https://`, which some web hosts require.
* Keep the address under 127 characters.

## Test it

From another computer, request a file that `fastdl` created:

```bash
curl -I http://203.0.113.10:8080/fastdl/maps/koth_example.bsp.bz2
```

`HTTP/1.1 200 OK` means the web server is working. Then join the server with a client that does not have the map. To see each download in the game console, enter `developer 1` and `download_debug 1` in the client console before joining.

## Troubleshooting

| Problem | Cause and fix |
| --- | --- |
| `403 Forbidden` | The web server cannot read the files. Run `sudo usermod -aG gameserver www-data` and restart the web server, or use [nginx in Docker](#option-1-nginx-in-docker). |
| `404 Not Found` | The address is wrong. Check that `sv_downloadurl` ends in `/fastdl` and that the file exists in `public_html/fastdl`. If the name differs only in upper or lower case, see [Make Webserver Case Insensitive](make-webserver-case-insensitive.md). |
| `curl` times out or the connection is refused | The port is blocked or the web server is not running. Check the firewall and cloud provider firewall, and that the container or service is running. |
| Players still download slowly from the game server | `sv_downloadurl` is not set or not loaded. Check it in the server console with `sv_downloadurl`, and that the file is in FastDL. Excluded paths are not, see [`fastdlexclude`](../commands/fastdl.md#excluding-paths). |
| Players get an old version of a file | Clients keep files they have already downloaded. Rename the file when you change it. |
