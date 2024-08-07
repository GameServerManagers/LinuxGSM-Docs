# IP Address

Depending upon the configuration of your server you may need to be more aware of its IP address configuration and how it relates to your game server.&#x20;

{% hint style="success" %}
This guide is not designed to be an in-depth guide to networking, instead focusing on parts relevant to game servers.
{% endhint %}

## Network Locations

Your game server can be hosted online using a server provider such as Linode or on a [local network](broken-reference) at home for either local-only LAN parties or allowing online players in through your router.&#x20;

### Internet (Public)

If your server is hosted on the internet using a server provider you should have been allocated a public internet IP address that will be accessible by everyone on the internet.&#x20;

### Local Networks (Private)&#x20;

Using a home server or virtual machine on your desktop is a great way to get started with LinuxGSM. However, a local network (LAN) may require a better understanding of networking equipment, how local IP addressing works, and technologies such as [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) and [NAT](https://en.wikipedia.org/wiki/Network_address_translation).

When a server is hosted on a local network it will be given a private IP address that is only accessible to other devices on your local network. This is fine if you want to get friends around host a game server for a good old-fashioned LAN party. But if you want to allow online players access to your local game server you will need to configure your home router's firewall and setup port forwarding using NAT.

## Network Interfaces

All computers will have some sort of physical or virtual [network interface](https://en.wikipedia.org/wiki/Network_interface) (ethernet, fiber optic, wi-fi) to connect to a network. On Linux, you can see your server's interfaces by using the following command.

```text
ip -o link show
```

Typically you may see (depending on distro) a `localhost` loopback interface and an `eth0` interface. The `eth0` (Ethernet) is used for your standard copper network cable and is what you will likely see. If you have multiple interfaces you may also see `eth1`, `eth2`, etc. More advanced setups can choose to bond together interfaces to work as one to increase bandwidth and resilience.&#x20;

## IP Address

An IP (Internet Protocol) address is a numerical label assigned to each device connected to a computer network that uses the Internet Protocol for communication. It serves two primary functions: host or network interface identification and location addressing. IP addresses enable devices to send and receive data within a network, facilitating communication and data transfer across the Internet.

1. **LAN IP Address:**

    - Example: 192.168.1.10
    - Explanation: In a typical home or office network, devices are often assigned private IP addresses within the range defined by the Internet Engineering Task Force (IETF) for private networks. The "192.168.1.10" address is an example of a private IP address commonly used within a LAN. Each device on the local network would have a unique private IP address for internal communication.

2. **Internet IP Address:**
    - Example: 203.0.113.45
    - Explanation: Internet IP addresses, also known as public IP addresses, are assigned by Internet Service Providers (ISPs) and are globally unique. The "203.0.113.45" address is an example of a public IP address. Websites, servers, and other devices connected to the Internet have public IP addresses that are used for communication between different networks on a global scale. These addresses are essential for routing data across the Internet.

### Virtual Private Networks

Some servers may be connected to a VPN (Virtual Private Network) using software such as Wireguard or OpenVPN. This normally creates its own interface that gets allocated an IP address. It is possible to use a VPN to create a private connection to a LAN server

## Tunneling

A relatively new technology is starting be become popular that allows applications hosted (think self-hosted web applications) on a private network to be accessed on the internet via a network "tunnel". This typically involves running a tunnel client in the private network that points to a specific internal IP and port. This bypasses the need to port forward on a router. Currently, there is a service called [playit.gg](https://playit.gg/) that is specifically designed for game servers. However other solutions may work.

## IP Address Allocation

Each network interface can be allocated an IP address either manually on the server or via DHCP. If you are using a provider an internet IP address is normally automatically allocated to your server. For a local network, your router DHCP server will allocate a local IP address. A local IP address can be reserved using DHCP or you can manually set an IP on the server.

Game Servers will typically _bind_ (attach a network socket) to all available IP addresses making the game server available on all networks. However, sometimes a particular IP address may need to be specified if you only want a particular network to access it or the game server requires it.

## Single Server IP Address

The simplest and most common server configuration will have one network interface and thus one IP address. When your game server starts it will simply listen and bind to this IP address.

## Multiple Server IP Addresses

Some servers will have multiple network interfaces available, allowing for multiple IP addresses to be assigned to your server. In this configuration, a server might listen and bind itself to all IP addresses or just one (depending on the game server).

### Multihome

If you have multiple interfaces you may choose to multihome your server. This simply means each interface is on a different network. For example, `eth0` is on the `192.168.0.0` network and `eth1` is on the `192.168.1.0` network and `wg0` (WireGuard VPN) is attached to `10.0.0.0`. While it is unlikely there is a specific use case for game servers to use multiple networks you need to be aware of what IP addresses your server is bound to.

## 0.0.0.0

The 0.0.0.0 IP is a meta-address means non-specific or all addresses. When you set up a game server you may notice the IP address 0.0.0.0 in command line parameters and settings. It is the default IP for game servers just signifies that the game server can bind to all available server IP addresses.&#x20;

{% hint style="success" %}
Unless a specific IP address is required the game server IP can be set to 0.0.0.0.
{% endhint %}
