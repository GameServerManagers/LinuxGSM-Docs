# Hytale

## Requirements

* A **Hytale account that owns the game**. It's needed even to download the dedicated server, and for the server itself to run.
* Java 25 (`openjdk-25-jre` on Debian/Ubuntu, `java-25-openjdk` on RHEL-based distros). LinuxGSM installs it as a dependency.
* At least 4 GB of RAM. The download is about 3.5 GB.

Hytale isn't on Steam. LinuxGSM downloads the server with Hytale's official `hytale-downloader`.

## Two One-Time Logins

A Hytale server needs two separate logins with your Hytale account. Each one is approved **once** in a browser, then saved and renewed automatically.

| Login | When | Saved in |
| ----- | ---- | -------- |
| **Downloader** | During `install` | `serverfiles/.hytale-downloader-credentials.json` |
| **Server** | On the first `start` | `serverfiles/Server/auth.enc` (encrypted) |

{% hint style="info" %}
Both files contain credentials for your Hytale account. Like `secrets-*.cfg`, they're included in LinuxGSM backups, so keep backups private.
{% endhint %}

The server login is encrypted with a key tied to the machine, so it only works on the machine (or container) where it was created. After restoring a backup on another machine, or re-creating a Docker container, the server can't read it and needs a new login. LinuxGSM detects this on start and shows a new server login URL.

## Installing

1. Create and install the server:

   ```
   ./linuxgsm.sh hytserver
   ./hytserver install
   ```

2. **Downloader login.** The install stops at **Hytale account login required** and shows a URL. Open it in a browser, log in with your Hytale account and approve the code. The install waits up to 15 minutes, then downloads and extracts the server.

3. Start the server:

   ```
   ./hytserver start
   ```

4. **Server login.** On the first start, LinuxGSM shows **Hytale server login required** with a URL, and sends it as an alert if [alerts](../alerts/README.md) are configured. Open the URL and approve it within 10 minutes. The server saves the login and restores it on every restart. LinuxGSM checks this on every start and shows a new URL whenever the server isn't logged in.

If the server login code expires, or you need to log in again, send the command to the server console and approve the code shown in the console log (`./hytserver console`):

```
./hytserver send "/auth login device"
```

## Docker

The flow is the same, but there's no terminal, so the login URLs appear in the container logs:

1. Start the container and follow its logs:

   ```
   docker logs -f hytserver
   ```

2. Approve the **downloader** login URL from the logs within 15 minutes. The install then completes.
3. When the server starts, approve the **server** login URL from the logs, or from your configured alert (Discord, ntfy and so on), within 10 minutes.

The **downloader** login is saved under `serverfiles` on the data volume, so re-creating or updating the container doesn't ask for it again. The **server** login is tied to the container, so after re-creating or updating the container, approve the new server login URL from the logs or your alert.

## Server Settings

The server creates `serverfiles/Server/config.json` on first start. Stop the server before editing it.

| Setting      | Description                        |
| ------------ | ---------------------------------- |
| `ServerName` | Name shown to players.             |
| `Password`   | Password to join. Empty for none.  |
| `MaxPlayers` | Maximum number of players.         |
| `MOTD`       | Message of the day.                |

`./hytserver details` shows the server name, password and max players from this file.

To use a different patchline (for example pre-release), set `hytalepatchline` in your LinuxGSM instance config.

## Ports

| Description | Port   | Protocol |
| ----------- | ------ | -------- |
| Game        | `5520` | UDP      |

To change the port, set `port` in your LinuxGSM instance config (`lgsm/config-lgsm/hytserver/hytserver.cfg`). It's passed to the server as `--bind`.

## Updates

`./hytserver update` and `./hytserver check-update` use the saved downloader login, so they run unattended, for example from cron or with `updateonstart="on"`. LinuxGSM keeps your world, `config.json`, mods, bans and the server login when it updates.

If the saved downloader login stops working, an unattended update fails within 5 minutes with a message, rather than waiting forever. Run `./hytserver update` in a terminal and approve the login again.

{% hint style="info" %}
The Hytale server also checks for updates itself, every hour. If it updates its own files, `./hytserver update` and `./hytserver check-update` warn that the server files are newer than LinuxGSM's record, and the next `./hytserver update` corrects it.
{% endhint %}
