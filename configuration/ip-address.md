# IP Address

Depending upon the configuration of your server you may need to be more aware of its IP address configuration and how it relates to your game server. 

{% hint style="success" %}
This guide is not designed to be an in-depth guide to networking, instead focusing on parts relevent to game servers.
{% endhint %}

## Internet Server vs Local Server

Your game server can be hosted online using a server provider such as Linode or for on a [local network](local-home-server.md) at your house for either local-only LAN parties or allow online players in though your router. 

## Network Interfaces

All computers will have some sort of network interface \(ethernet, fibre optic, wi-fi\) to connect to a network. On Linux you can see your servers interfaces by using the following command.

```text
ip -o link show
```

Typically you may see \(depending on distro\) a `localhost` loopback interface and an `eth0` interface. The `eth0` \(ethernet\) is used for your standard copper network cable and is what you will likely see. It is possible to use multiple interfaces individually or for more a advanced setup can be bonded together work as one interface to increase bandwidth and resilience. 

## IP Address Allocation

Each network interface can be allocated an IP address either manually on the server or via DHCP. If you are using a provider an internet IP address is normally automatically allocated to your server. For a local network, your router DHCP server will allocate a local IP address. A local IP address can be reserved using DHCP or you can manually set an IP on the server.

## Single Server IP Address

The simplest and most common server configuration will have one network interface and thus one IP address. When your game server starts it will simply listen and bind to this IP address.

## Multiple Server IP Addresses

Some servers will have multiple interfaces available and allow for multiple IP addresses to be assigned to it. In this configuration a server can listen and bind itself all IP addresses or just one.

## 0.0.0.0

The 0.0.0.0 IP is a meta-address means non-specific or all addresses. When you setup a game server you may notice the IP address 0.0.0.0 in command line parameters and settings. It is the default IP for game servers just signifies that the game server can listen and use all available server IP addresses. 

{% hint style="success" %}
Unless a specific IP address is required the game server IP can be set to 0.0.0.0.
{% endhint %}

## Internet

If your server is hosted online you will have been allocated a public internet IP address that will be accessible by everyone online. Depending upon your server you may only need to configure your server firewall to open ports your game server uses.

## Local Networks

Using a home server or virtual machine on your desktop is a great way to get started with LinuxGSM. However, a local network may require a better understanding of networking, how local IP addressing works and technologies such as DHCP and NAT.

When a server is hosted on a local network it will be given a private IP address that is only accessible to other devices on your local network. This is fine if you want to get friends around host a game server for a good old fashioned LAN party. But if you want to allow online players access to your local game server you will need to configure your home router's firewall and setup port forwarding using NAT.

How LinuxGSM handles IP addresses

By default, LinuxGSM will use the 0.0.0.0 meta-address allowing all IP addresses to be automaticly used. LinuxGSM gathers various IP address information to try and automaticly determine the correct IP address to query, and what to display in `details` and notifications. 

If a specific IP address is required you can set it using the `ip` setting in the LinuxGSM or game server config files. The same also applies if you wish to change the IP address of server noficiations you can use the [displayip](../alerts/#display-ip).

