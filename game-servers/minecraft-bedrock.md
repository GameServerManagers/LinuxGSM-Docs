# Minecraft Bedrock

## Requirements

- An x86-64 Linux server. Mojang only publishes a Linux build of Bedrock Dedicated Server (BDS) for x86-64.
- The server files come from Mojang's download API, not SteamCMD.

## NetherNet

From version 26.50, BDS uses a new network transport called NetherNet by default. Older versions used RakNet. NetherNet changes which ports the server uses and how tools can check that it's online.

- `server-port` (default `19132`) is now a **TCP** port. Clients use it for signalling, the first handshake before they join.
- Gameplay traffic runs over **UDP** ports that the server and client agree on during signalling. If you don't set them, the server picks random ports, which you can't open in a firewall in advance. Pin them with `server-udp-ports`.
- `server-portv6` is ignored.
- The transport is set by `transport` in `server.properties`. When the line is missing, BDS uses NetherNet.

{% hint style="warning" %}
Don't switch back with `transport=raknet`. RakNet is deprecated: the server logs `NetherNet is the only supported transport type. Players will not be able to connect`. Query tools would see the server again, but players couldn't join it.
{% endhint %}

## Server Settings

The game settings are in:

```
serverfiles/server.properties
```

Restart the server after editing it. Updates don't replace `server.properties`, `permissions.json` or `allowlist.json`.

Network settings for NetherNet:

| Setting            | Example         | Description                                                                          |
| ------------------ | --------------- | ------------------------------------------------------------------------------------ |
| `server-port`      | `19132`         | TCP signalling port.                                                                 |
| `server-udp-ports` | `19132`         | UDP port, or range of ports, for gameplay. Without it, the server uses random ports. |
| `transport`        | `nethernet`     | Network transport. Leave it unset or set it to `nethernet`.                          |
| `server-name`      | `LinuxGSM`      | Name shown in the server list and in query results.                                  |
| `level-name`       | `Bedrock level` | World folder name.                                                                   |
| `max-players`      | `10`            | Maximum players.                                                                     |

The instance config is `lgsm/config-lgsm/mcbserver/mcbserver.cfg`:

| Setting     | Default  | Description                                                              |
| ----------- | -------- | ------------------------------------------------------------------------ |
| `mcversion` | `latest` | `latest` for the newest release, `preview` for the newest preview build. |

## Ports

| Description                | Port                     | Protocol |
| -------------------------- | ------------------------ | -------- |
| Signalling (`server-port`) | `19132`                  | TCP      |
| Game (`server-udp-ports`)  | `19132` (if set to this) | UDP      |
| LAN discovery              | `7551`                   | UDP      |

TCP and UDP don't clash, so `server-udp-ports` can use the same number as `server-port`. Open both in your firewall:

- TCP `server-port`.
- UDP `server-udp-ports`, the whole range if you set one.
- UDP `7551` is only used to show the server in the LAN games list for players on the same network. You don't need to open it to the internet.

To run more than one instance on a host, give each its own `server-port` and `server-udp-ports`.

### Docker

Publish the signalling port as TCP and the game ports as UDP. Keep the host and container port numbers the same, because the server tells clients which port to use. For example, with `server-port=19132` and `server-udp-ports=19132`:

```
ports:
  - "19132:19132/tcp"
  - "19132:19132/udp"
```

A config that only publishes `19132/udp` worked with RakNet, but with NetherNet the server is unreachable.

## Monitor and Query

BDS no longer answers the RakNet query on UDP `server-port`. Tools that only send that query (older GameDig, many server list sites and status bots) show a NetherNet server as offline even when it's running.

LinuxGSM's `monitor` checks that the TCP `server-port` accepts connections. That shows the server is up and listening, but it can't tell a hung server from a working one. See [monitor](../commands/monitor.md).

The signalling port also answers a plain HTTP request with the server status, without logging in:

```
curl http://<ip>:19132/v1/join
```

```
{"name":"LinuxGSM","protocol":2225,"version":"1.26.63","level":"Bedrock level","players":0,"maxPlayers":10,"gameType":0}
```

It gives the server name, version, world name and player counts. BDS has no separate MOTD. The server name is what players see.

## Updates

LinuxGSM checks Mojang's download API for the newest Linux build and compares it with the version in the console log. Players need a client version that matches the server.

## Server Resources

- [Bedrock Dedicated Server](https://www.minecraft.net/en-us/download/server/bedrock)
- [server.properties reference](https://learn.microsoft.com/en-us/minecraft/creator/documents/bedrockserver/server-properties)
- [Bedrock Dedicated Server on the Minecraft Wiki](https://minecraft.wiki/w/Bedrock_Dedicated_Server)
