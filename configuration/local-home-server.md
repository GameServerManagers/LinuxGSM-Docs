# Local/Home Server

WIP

## Home Servers

Home servers are a great way to experiment with game servers, for LAN parties or can be used as a permanent option if you have the bandwidth. There are extra steps required on your home router to allow external access to your game server. This will normally involve opening ports on the router's firewall and/or port forwarding. See [this link](https://www.howtogeek.com/66214/how-to-forward-ports-on-your-router/) for basic instructions. See your router's documentation for specific instructions.

### Specifying your IP for Home Server

If you want to specify the game server IP address using the `ip=` you will need to set the IP address of the server's LAN interface (e.g. 192.168.1.2), not your router's external IP. Setting this incorrectly will prevent the game server ports from binding and your server will not start.
