# fastdl

FastDL (Fast Download) allows the client to download custom server content (maps, materials, models, particles, sounds, fonts, images) from a web server.

It is used to offload content downloads to a web server instead of relying on source servers (SRCDS) that only allows 20KBps downloads to clients. Content on the web server can be compressed to further speed up the download process. This means that custom content downloads much faster.

Valve now use [Steam Workshop](../steamcmd/workshop.md) for most custom content however FastDL is still required in some cases.

LinuxGSM FastDL automatically creates the web directories and compresses the content for you. After the first run, it only updates the files that have changed.

## Supported Servers

* All Source engine servers, including Garry's Mod
* All GoldSrc servers

## Commands

Standard: `./gameserver fastdl`

Short: `./gameserver fd`

## How it works

Each time `fastdl` runs it:

1. Gathers the files clients may need from the game server, including Source `custom` folders.
2. Works out what has changed since the last run and shows a summary.
3. Asks `Continue?` before changing anything.
4. Removes files it added before whose source is no longer on the server.
5. Copies new and changed files, then compresses them with bzip2 (Source only).
6. Generates the download enforcer (Garry's Mod only).

The summary looks like this:

```
found 1532 files: 1497 unchanged, 12 excluded, 3 duplicate
about to update 20 files, 20 to compress, total size 48 MB
about to remove 2 files no longer on the server
3 files in the Fastdl directory were not added by tf2server and will be left alone
```

### Files collected

#### Source

| Folder | File types |
| --- | --- |
| `maps` | .bsp .ain .nav .jpg .txt |
| `materials` | .vtf .vmt .vbf .png .svg |
| `models` | .vtx .vvd .mdl .phy .jpg .png .vmt .vtf |
| `particles` | .pcf |
| `sound` | .wav .mp3 .ogg |
| `resource` | all files |

#### Source custom folders

Content in the game's `custom/<name>/` folders is collected too, using the same folders and file types. Files are placed at the path the client asks for, without the `custom/<name>/` part:

```
tf/custom/mymaps/maps/koth_example.bsp  ->  fastdl/maps/koth_example.bsp.bz2
```

If the same file exists in more than one place, LinuxGSM uses the same order as the game server: `custom` folders come before the game's own folders, and `custom` folders are checked in name order. The copies that are not used are listed in the LinuxGSM script log.

#### Garry's Mod

Garry's Mod collects these file types from anywhere in the `garrysmod` folder: .ain .bsp .mdl .mp3 .ogg .otf .pcf .phy .png .svg .vtf .vmt .vtx .vvd .ttf .wav.

* Content in `addons/<name>/` is placed without the `addons/<name>/` part, for example `addons/mymod/models/car.mdl` goes to `models/car.mdl`.
* Content in `lua/` is also placed without the `lua/` part.

#### GoldSrc

| Folder | File types |
| --- | --- |
| Game folder (top level only) | .wad |
| `maps` | .bsp .res .txt |
| `models` | .mdl |
| `sound` | .wav |
| `sprites` | .spr .txt |
| `gfx` | .tga .bmp |
| `overviews` | .bmp .tga .txt |

### Updating FastDL

Run `fastdl` again whenever server content is added, changed or removed. Only the differences are applied:

* New files are copied and compressed.
* A file is updated when its source changes size or modification time, or when a different copy of it takes over (for example a `custom` folder copy is removed and the game's own copy is used instead).
* Files LinuxGSM added are removed when their source is no longer on the server.
* Unchanged files are left as they are, so later runs do not recompress everything.

LinuxGSM keeps a record of the files it has written in `lgsm/data/<gameserver>-fastdl.txt`, for example `lgsm/data/tf2server-fastdl.txt`. This is how it knows what has changed and which files it is allowed to remove.

{% hint style="info" %}
Clients will not download a file they already have unless its name changes. If you change a map or other content that players already have, rename it.
{% endhint %}

### Files you add to the FastDL directory

LinuxGSM only removes files that it added itself. Anything else in the FastDL directory, such as an `index.html`, a `.htaccess` file, or files uploaded by hand, is left alone and reported in the summary.

This also means several game servers can share one FastDL directory. Each server only removes its own files. If two servers provide the same file and one of them stops providing it, run `fastdl` on the other server again to put it back.

{% hint style="warning" %}
When you answer **Yes** to `Rebuild Fastdl directory from scratch?`, LinuxGSM deletes **everything** in the FastDL directory, including files you added yourself, and then rebuilds it. The default answer is **No**.
{% endhint %}

If you used `fastdl` before LinuxGSM kept a record, the first run updates all files once. Old files from earlier runs that no longer have a source on the server are reported as left alone rather than removed. Rebuild from scratch once, or delete them yourself, to clear them.

## Settings

Settings are added to `common.cfg` or the instance config. See [LinuxGSM Config](../configuration/linuxgsm-config.md).

### Excluding paths

`fastdlexclude` lists paths to leave out of FastDL. The paths are relative to the FastDL directory and separated by spaces. Any file whose path starts with one of them is skipped, and wildcards such as `*` can be used.

Source servers exclude Workshop maps by default, because players download those from the Workshop:

```properties
fastdlexclude="maps/workshop/"
```

To also leave out a folder of large music files and all navigation meshes:

```properties
fastdlexclude="maps/workshop/ sound/music/ *.nav"
```

Excluded files that are already in the FastDL directory are removed on the next run, as long as LinuxGSM added them.

### Web directory

FastDL files are created in `public_html/fastdl` inside the LinuxGSM installation directory. To use a different location, set `webdir`. The files are then created in `fastdl` inside that directory.

```properties
webdir="/var/www/html"
```

## Serving the files

Players download FastDL files from a web server, which LinuxGSM does not set up for you. Any web server that can serve static files works, such as nginx or Apache, on the game server or on a separate web host.

See the [FastDL Web Server](../guides/fastdl-web-server.md) guide for step-by-step setups with nginx or Apache, in Docker or installed on the server, plus testing and troubleshooting.

The quickest option, if Docker is installed, serves the files on port 8080:

```bash
docker run -d --name fastdl --restart unless-stopped -p 8080:80 \
  -v /home/gameserver/public_html:/usr/share/nginx/html:ro nginx:stable
```

Then add the address of the `fastdl` folder to the [game server config](../configuration/game-server-config.md) and restart the game server:

```
sv_downloadurl "http://203.0.113.10:8080/fastdl"
sv_allowdownload 1
```

## Bzip2 Compression

Source servers compress FastDL content with bzip2, which Source games support, so client downloads are faster. It is a must-have if you're hosting large files, as it will save you bandwidth, and speed up downloads for clients. However, using bzip2 on many small files can slow down client loading times.

LinuxGSM compresses several files at once, one per CPU core, so large servers finish much faster. Files larger than 150 MB are copied without compression, because Source clients will not download a compressed file that large.

GoldSrc does not support bzip2 compression, so GoldSrc files are copied as they are.

## Garry's Mod Download enforcer

In order for a client to download files from a FastDL in Garry's Mod, the developer of an addon must put files from the addon into lua code `resource.Addfile ( "/path/to/file.ext" )`. However, some addon developers do not do this. In order for clients to download the required files, an lua file needs to be generated for it to work, which is what the lua enforcer feature does. The only downside is that clients may download files that are not required on the server.

When `fastdl` asks `Force clients to download files?`, answer **Yes** to generate `garrysmod/lua/autorun/server/lgsm_cl_force_fastdl.lua`. It lists every file LinuxGSM adds to FastDL and is regenerated each run. Answer **No** to remove it.
