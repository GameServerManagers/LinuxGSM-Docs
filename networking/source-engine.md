# Source Engine

## Default ports

Source engine servers use the following ports by default.

| Port     | Default | Protocol | Direction       | Open or forward it?             |
| -------- | ------- | -------- | --------------- | ------------------------------- |
| Game     | 27015   | UDP      | Inbound         | Yes                             |
| Query    | 27015   | UDP      | Inbound         | Yes (same port as the game)     |
| RCON     | 27015   | TCP      | Inbound         | Only if you use RCON remotely   |
| SourceTV | 27020   | UDP      | Inbound         | Only if SourceTV is enabled     |
| Client   | 27005   | UDP      | Unused          | No, but it must be unique       |

GoldSrc engine servers (Half-Life 1 based games) use 27015 for the game, query and RCON, and do not open a client port.

## Client port

The client port is the one that confuses most people, so here is what it is and why LinuxGSM sets it.

### What it is

The Source engine is a single program that contains both the game you play and the server you host. When you play a Source game, the client half of the engine uses the client port (27005 by default) to talk to servers. A dedicated server runs the same engine, so it opens the client port as well, even though no player is sitting at it.

<figure><img src="../.gitbook/assets/source-client-port-halves.svg" alt="A Source server has a server half on port 27015 that players and the server browser connect to, and an unused client half on port 27005"><figcaption><p>Players and the server browser only ever use the game port</p></figcaption></figure>

On a dedicated server the client port is unused. Players, server browser queries, RCON and the Steam master server do not use it, and nothing is sent or received on it. It does **not** need to be opened in a firewall or forwarded on a router.

### Why it still matters

Even an unused port takes up its number, and only one program can use a port number at a time. If you run more than one Source server on the same host, each server needs its own client port, as well as its own game and SourceTV ports.

LinuxGSM starts Source servers with `-strictportbind`, which tells the server to stop rather than quietly pick a different port. So if a second server finds 27005 already taken, it will not start, even when its game port is different. The console log shows:

```
FATAL ERROR: ERROR: Port 27005 was unavailable - quitting due to "-strictportbind" command-line flag!
```

<figure><img src="../.gitbook/assets/source-client-port-two-servers.svg" alt="Server A takes client port 27005 and runs. Server B with the same client port fails. Server B with client port 27006 runs"><figcaption><p>Two servers on one host need different client ports</p></figcaption></figure>

To fix it, give each server its own client port in its [instance config](../configuration/linuxgsm-config.md):

```
clientport="27006"
```

See [Ports](ports.md) for ways to plan ports across several servers.

{% hint style="info" %}
Servers that each run in their own Docker container have their own set of ports, so they cannot clash on the client port.
{% endhint %}

### Games that ignore it

A few Source games handle the client port differently. Setting `clientport` has no effect on them:

* **Garry's Mod** picks a random client port each time it starts.
* **Left 4 Dead**, **Left 4 Dead 2** and **Nuclear Dawn** do not open a client port at all.

## Static Port Mapping (NAT/Docker)

The port that is configured in the start parameters _must_ be the port that is exposed to the Internet. This is because the game server reports the port that it is configured in start parameters to use to the master server. If this does not match the game client will not be able to connect to the server.

<figure><img src="../.gitbook/assets/srcds_ports.jpg" alt=""><figcaption><p>Changing port using Docker or firewall</p></figcaption></figure>

<figure><img src="../.gitbook/assets/sdcds_ports_2.jpg" alt=""><figcaption><p>Changing port using the start parameters</p></figcaption></figure>
