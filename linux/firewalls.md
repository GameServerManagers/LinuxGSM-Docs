# Firewalls
A firewall is a security device that blocks or allows network traffic on to a system or network to prevent unauthorised access and help protect from malicious attack.
Firewalls can also assist in rate limiting traffic to prevent too much traffic being sent to a system. This is useful for game servers to help prevent a DoS (Denial of Service) attack that can overwhelm a game server.

Firewalls can be physical hardware devices that sit on a network, or software that sits on a server or desktop device. This page will focus mainly on software firewalls.

## DDoS protection
A [distributed denial-of-service](https://en.wikipedia.org/wiki/Denial-of-service_attack (DDoS) attack occurs when multiple systems flood the bandwidth or resources of a targeted system, usually one or more web servers. Such an attack is often the result of multiple compromised systems (for example, a botnet) flooding the targeted system with traffic. A botnet is a network of zombie computers programmed to receive commands without the owners' knowledge.
Server providers may offer DDoS protection, such as Arbor, that will mitigate such attacks before it reaches a server. However this feature is often provided as a premium feature meaning often only available on more expensive servers. Some providers may also provided sub-standard protection that may incorrectly filter traffic. So be aware of what protection if any a server provider has to protect your server.

### iptables
[iptables](http://ipset.netfilter.org/iptables.man.html) is the most commonly used and supported Linux firewall utility, with many other tools interfacing with it
To see iptables rules: `iptables -L` To flush \(erase\) iptables rules: `iptables -F`

### Protecting a game server
One way to protect a game server is to rate limit incoming connections to the game server. Iptables will do this by dropping packets from a connection if it is sending too much traffic.
This is particularly important if using the LinuxGSM monitor feature, as monitor relies on the query port being available. Should the query port be flooded with traffic it may become unavailable and LinuxGSM will assume the game server has crashed and reboot. 
The below example will rate limit traffic on port 27015 (the default for source engine games) to 10 requests every 60 seconds. Different game servers may require different rate limits, so it may be important to adjust the limits to ensure legitimate traffic does not get blocked.
```
iptables -A INPUT -p udp -m udp --dport 27015 -m state --state NEW -m recent --set --name DEFAULT --rsource
iptables -A INPUT -p udp -m udp --dport 27015 -m state --state NEW -m recent --update --seconds 60 --hitcount 10 --name DEFAULT --rsource -j DROP
```

### Checking connectivity

Once you have created your port forwards and want to see if the internet can access the ports, there is a website called [canyouseeme.org](http://www.canyouseeme.org). Simply change the port to your game port \(27015 for example\) and it will tell you if it can access it on your computer. This will help you verify your port forward was created successfully.

### Networks with multiple gateways

Some game servers \(like Rust\) register their external IP with steam when they start up. When you create port forwards to the game server, you need to make sure the port forward is on the address the outbound traffic is on. For example, say you have a router with two IPs from different ISPs;

```text
[eth0] 192.168.1.1 (LAN)
     |  |
-----------------
|                | --[WAN0] 71.2.5.23 (ISP A)  
|                | --[WAN1] 65.13.29.46 (ISP B)  
------------------
```

If your traffic is going out WAN0 you need to put the port forwards on the 71.2.5.23 address. If your outbound traffic is going out WAN1 you would need to put your port forwards on 65.13.29.46.

#### More rules to come. Feel free to edit this wiki if you know more.

