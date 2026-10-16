# Source Engine

## Default ports

These are common defaults for Source dedicated servers. The game, engine version and start parameters determine the actual ports; GoldSrc and Source 2 games may differ.

| Purpose | Common default | Protocol | Use |
| --- | --- | --- | --- |
| Game and query | 27015 | UDP | Player connections and server browser queries. |
| RCON | 27015 | TCP | Remote administration, if needed. |
| Client | 27005 | UDP | The engine's client networking socket. |
| SourceTV | 27020 | UDP | Spectator traffic when SourceTV is enabled. |
| Steam backend | Around 26900/26901 | UDP on older Source servers | Communication with Steam services; the port may be selected automatically. |

Check the game's documentation and `./gameserver details` before setting firewall or Docker port mappings. You do not need to expose every port in this table for every server.

## Steam backend port

Valve describes the [Steam port](https://partner.steamgames.com/doc/api/steam_gameserver#SteamGameServer_Init) as the local port used to communicate with Steam servers. It is separate from the game port and query port. A [Game Server Login Token](../steamcmd/gslt.md) authenticates the server; it does not assign a universal GSLT port.

Older Source games commonly use ports around 26900/26901, and some select another port when one is occupied. Supported launch options and the relationship between a requested port and the bound port vary by game. Check the game's supported start parameters before changing this port. A LinuxGSM variable only changes the binding if the game's launch command or config uses it.

LinuxGSM can report a configured Steam port and may detect one from a running Source server's sockets. If the port is unknown, the Steam row may be absent. This alone does not show that Steam login has failed.

## Firewall direction and port forwarding

Allow incoming game/query traffic on the ports players use. Allow SourceTV traffic if you offer it, and restrict RCON access to trusted administrators.

Steam backend communication also needs the required outbound access and reply traffic. On a stateful firewall, replies to an allowed outbound connection are normally permitted. Do not add an inbound forwarding rule for 26901 just because a server uses GSLT. If Steam login fails, check the game console and the game's networking requirements before changing firewall rules.

SteamCMD login/download connections have separate requirements; see [SteamCMD network ports](../steamcmd/README.md#network-ports) and Valve's [Required Ports for Steam](https://help.steampowered.com/en/faqs/view/2EA8-4D75-DA21-31EB).

## Static Port Mapping (NAT/Docker)

The port that is configured in the start parameters _must_ be the port that is exposed to the Internet. This is because the game server reports the port that it is configured in start parameters to use to the master server. If this does not match the game client will not be able to connect to the server.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      &#x20;

<figure><img src="../.gitbook/assets/srcds_ports.jpg" alt=""><figcaption><p>Changing port using Docker or firewall</p></figcaption></figure>



<figure><img src="../.gitbook/assets/sdcds_ports_2.jpg" alt=""><figcaption><p>Changing port using the start parameters</p></figcaption></figure>

