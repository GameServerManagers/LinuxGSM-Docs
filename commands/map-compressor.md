# map-compressor

The `map-compressor` command compresses custom content for some Unreal engine servers, so clients can download it quickly from a web server (HTTP redirect).

Stock game content is skipped, because clients already have it. Only custom content is compressed: maps, mods, textures, sounds and other packages you have added. LinuxGSM recognises stock content by name and checksum, so a stock file that a mod has replaced is still compressed.

## Supported Servers

* Unreal Tournament 99
* Unreal Tournament 2004
* Killing Floor
* Red Orchestra

## Commands

Standard: `./gameserver map-compressor`

Short: `./gameserver mc`

## Supported file formats

* Maps (.unr, .ut2, .rom, .kfm)
* Code packages (.u)
* Textures (.utx)
* Sounds (.uax)
* Music (.umx)
* Static meshes (.usx)
* Animations (.ukx)

Unreal Tournament 99 files are compressed to `.uz`. Unreal Engine 2 games use `.uz2`.

## Usage

Run `./gameserver mc`. Compressed files are saved to `Maps-Compressed` in the LinuxGSM root directory. To change this, set `compressedmapsdir` in your LinuxGSM config.

Runs are incremental. A file is only compressed again if it has changed, and compressed files whose source has been removed are deleted. Keep only `map-compressor` output in this directory.

If a file fails to compress, the other files are still processed and the failed files are listed at the end.

## Setting up the redirect

Upload the contents of the compressed files directory to a web server. Then set the following in your game server config:

```ini
[IpDrv.HTTPDownload]
RedirectToURL=http://example.com/path/
UseCompression=True
```
