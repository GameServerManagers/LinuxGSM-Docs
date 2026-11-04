# Minecraft: CurseForge

CurseForge Minecraft support in LinuxGSM uses a dedicated server target: `cfmcserver` (`shortname=cfmc`).

It is designed for pinned, deterministic server-pack updates instead of tracking a floating "latest" pack.

## Java Requirements

`cfmcserver` uses Java, like other Minecraft Java targets in LinuxGSM.

Install Java from LinuxGSM dependencies and make sure the installed Java version matches your modpack requirements.

## Installing a CurseForge Server Pack

Create the server script:

```bash
./linuxgsm.sh cfmcserver
```

Then install:

```bash
./cfmcserver install
```

For unattended install:

```bash
./cfmcserver auto-install
```

## Server Configuration

Configuration for CurseForge Minecraft is set in LinuxGSM config files.

Useful references:

* [LinuxGSM config](../configuration/linuxgsm-config.md)
* [Start parameters](../configuration/start-parameters.md)
* [install command](../commands/install.md)
* [update command](../commands/update.md)
* [check-update command](../commands/check-update.md)

### LinuxGSM Server Config

Main config file:

```bash
lgsm/config-lgsm/cfmcserver/cfmcserver.cfg
```

Example API mode configuration:

```text
cfmcsource="api"
curseforgemodid="123456"
curseforgefileid="654321"
cfmcstartmode="auto"
cfmcpreservepaths=""
```

Variable summary:

* `cfmcsource` - source mode: `api` or `url` (default `api`)
* `curseforgemodid` - CurseForge project/mod ID
* `curseforgefileid` - CurseForge file ID
* `curseforgeurl` - direct archive URL, local archive path, or CurseForge file-page URL
* `cfmcstartmode` - startup detection mode: `auto` or `manual`
* `cfmcpreservepaths` - extra preserve paths separated by semicolons

### Secrets Config

Set API key in a secrets file:

```bash
lgsm/config-lgsm/cfmcserver/secrets-common.cfg
```

or:

```bash
lgsm/config-lgsm/cfmcserver/secrets-cfmcserver.cfg
```

Example:

```text
curseforgeapikey="YOUR_CURSEFORGE_API_KEY"
```

### Get a CurseForge API Key

1. Sign in to the CurseForge API console:
   * https://console.curseforge.com/#/api-keys
2. Create a new API key.
3. Copy the key value.
4. Add it to:
   * `lgsm/config-lgsm/cfmcserver/secrets-common.cfg`
   * or `lgsm/config-lgsm/cfmcserver/secrets-cfmcserver.cfg`

Keep this key in a secrets file only and do not commit it to git.

## Source Modes

### API Mode

`api` mode is the recommended mode for pinned updates.

Required values:

* `curseforgemodid`
* `curseforgefileid`
* `curseforgeapikey`

LinuxGSM queries the CurseForge API for the file and uses `serverPackFileId` when it exists.

### URL Mode

`url` mode can use:

* direct archive URL
* local archive path
* CurseForge web file URL that contains `/files/<id>`

Example URL mode:

```text
cfmcsource="url"
curseforgeurl="https://example.org/my-modpack-server.zip"
cfmcstartmode="auto"
```

If `curseforgeurl` points to a CurseForge web file URL, LinuxGSM resolves download metadata through the API and requires:

* `curseforgemodid`
* `curseforgeapikey`

## Update Behavior

### Deterministic Build Marker

`serverfiles/build.txt` stores the current installed source marker.

Format:

* API mode: `cfapi:<modid>:<resolved_serverpack_fileid>`
* URL mode: `cfurl:<sha1(url)>`

This marker is used by:

* `./cfmcserver check-update`
* `./cfmcserver update`

### Preserve/Restore During Updates

CurseForge pack updates are applied as an overlay extraction. LinuxGSM preserves and restores common server data automatically.

Default preserve set:

* world from `level-name` in `server.properties`:
  * `<level>`
  * `<level>_nether`
  * `<level>_the_end`
* customization/data directories:
  * `local/`
  * `journeymap/`
  * `kubejs/`
  * `serverconfig/`
* core identity/admin files:
  * `server.properties`
  * `eula.txt`
  * `ops.json`
  * `whitelist.json`
  * `banned-ips.json`
  * `banned-players.json`
  * `usercache.json`

Add extra preserve paths with `cfmcpreservepaths` using semicolon separators.

## Startup Detection

When `cfmcstartmode="auto"`, LinuxGSM checks for pack start scripts in this order:

1. `startserver.sh`
2. `start.sh`
3. `run.sh`

If none are found, it falls back to launching a detected `.jar`.

Detected values are written to:

```bash
lgsm/config-lgsm/cfmcserver/cfmcserver.cfg
```

Updated keys:

* `preexecutable`
* `executable`
* `startparameters`

Set `cfmcstartmode="manual"` to keep custom startup settings unchanged.

## Common Commands

```bash
./cfmcserver start
./cfmcserver stop
./cfmcserver restart
./cfmcserver details
./cfmcserver check-update
./cfmcserver update
```

To force a re-apply of the configured source marker, run:

```bash
forceupdate=1 ./cfmcserver update
```

## Troubleshooting

### Missing required settings

Install/update fails fast when required CurseForge values are missing and reports which file to edit.

### API key not being used

Check:

* `lgsm/config-lgsm/cfmcserver/secrets-common.cfg`
* `lgsm/config-lgsm/cfmcserver/secrets-cfmcserver.cfg`

### CurseForge URL rejected in URL mode

Use one of:

* direct archive URL
* local archive path
* CurseForge URL containing `/files/<id>`

### Default game config download is skipped

`cfmcserver` does not fetch external default game config files and uses `servercfgdefault=""` by design.
