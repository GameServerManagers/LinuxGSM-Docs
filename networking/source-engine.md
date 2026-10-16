# Source Engine

## Default ports

For a typical public Source dedicated server, allow **27015/UDP inbound** for players and server browser queries. If the server is behind a router, forward that port to the server. Add incoming ports for RCON or SourceTV only when you use those services over the Internet.

The table shows common Source defaults. Use your configured ports if they differ, and check the game's requirements for additional services. GoldSrc and Source 2 games may differ.

Direction is relative to your server: **Inbound** starts with another machine contacting your server; **Outbound** starts with your server contacting another service. Replies travel in the opposite direction.

| Purpose | Default port | Protocol | Direction | Forward on the router? |
| --- | --- | --- | --- | --- |
| Game and query | 27015 | UDP | **Inbound** | **Yes**, for Internet players and queries. |
| RCON | 27015 | TCP | **Inbound** | **Only if** administrators need direct Internet access. Restrict it to trusted addresses. |
| SourceTV | 27020 | UDP | **Inbound** | **Only if** Internet spectators use SourceTV. |
| Client networking | 27005 | UDP | **Outbound** | **No** for normal dedicated Source server hosting. |
| Steam backend | 26900/26901 on older Source games; varies | UDP | **Outbound** | **No** for outgoing Steam connections and their replies. |

The forwarding guidance assumes a router with stateful NAT and outbound connections allowed. The router tracks outbound connections and lets their replies back without a separate port forward.

## Firewall and router setup

* **Server firewall:** allow the inbound game/query port and any optional incoming services you use. Allow required outbound Steam traffic and its replies.
* **Router/NAT:** forward only the required incoming services to the server. Outbound Steam connections and their replies do not need manual forwarding rules.
* **Public-IP server/VPS:** router forwarding is not needed when the server has a directly reachable public IP. The server firewall and provider firewall/security group must still allow the required incoming traffic.
* **Docker bridge networking:** publish the required incoming ports to the host with the correct TCP/UDP protocol. If the host is behind a router, forward those ports to the host as well. Outbound connections do not need Docker ports published to receive replies.

Use `./gameserver details` to check port settings. Its `LISTEN` column reports socket binding; it does not test firewall rules, router forwarding or Internet reachability. If Steam login fails, check the game console and outbound connectivity rather than adding an inbound Steam-port forward.

## Static Port Mapping (NAT/Docker)

Source servers advertise their configured game port to Steam's server browser. Keep the Internet-facing game port the same as the game's configured port so players can connect to the advertised address.

For example, if the game uses 27015/UDP, publish 27015/UDP from Docker and forward 27015/UDP on the router to that host. To use 27016/UDP instead, change the game's start parameters to 27016 and use that port in the Docker mapping and router rule.

<figure><img src="../.gitbook/assets/srcds_ports.jpg" alt=""><figcaption><p>Changing port using Docker or firewall</p></figcaption></figure>



<figure><img src="../.gitbook/assets/sdcds_ports_2.jpg" alt=""><figcaption><p>Changing port using the start parameters</p></figcaption></figure>

