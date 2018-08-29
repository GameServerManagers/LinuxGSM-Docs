# Firewalls

## What are firewalls ?

Firewalls are part of a very complex topic, but let's try to sum up their purposes, usages, and limits.

The main idea is to prevent certain kind of connections to happen, whether it's incoming our outgoing, IP and port restriction, or requests quotas. The goal is to protect against some sorts of hacking and DDoS.  
However the main downside is that unless you're using a very restrictive firewall, you'll probably just waste time rather than protect yourself against anything. For example, say you disallow any incoming connection to everything that isn't important, and leave everything important open to any IP without any restrictions \(which is a common practice\), then you just wasted your time. Why ? Because you didn't change anything compared to the previous behavior. In this case, you'd better make sure that what's listening is secured and "voilà".  
On the other hand, if you're only allowing certain IPs on certain ports, then your server is secured as hell, but almost nobody can connect to it.

Firewalls can be hardware or software. Here, we're only going to talk about software firewalls, and especially, iptables.

When your server gets popular, chances are some people will try to interrupt your services using DDoS. If your server provider doesn't have an efficient hardware based anti-DDoS protection, a common solution is to try detecting DDoS with firewall rules and drop their packets to prevent your services from being shut down.

There are some good practices that might help getting your servers more reliable. Here are some of them.

### iptables

[iptables](http://ipset.netfilter.org/iptables.man.html) is the most used and supported Linux firewall. You'll find plenty of documentations all over the web. Firewall settings usually gets reset on a reboot, which is a good thing, because if you mess with your config and can't connect anymore, you can still "just" reboot your machine. People usually make very basic scripts to apply the firewall settings back easily, and eventually start it on server boot. But protip: Whatever you do, make sure to test a firewall setting before setting it on boot, because you might make an error, preventing you from connecting back to your machine... Don't laugh, i'm pretty sure it's not a legend, it might happen.

To see iptables rules: `iptables -L` To flush \(erase\) iptables rules: `iptables -F`

## DDoS protection

As a reminder, a [distributed denial-of-service](https://en.wikipedia.org/wiki/Denial-of-service_attack) is the most retarded attack you could be subjected to, yet it can be very annoying, as the idea is to flood your server with enough corrupted requests to prevent it from answering properly to useful ones.

Server providers may offer DDoS protections, like Arbor, that will allow you to not even notice most DDoS, unless the attacker have a really huge attack force, which is unlikely. On the other hand, what's likely is that your server provider that you're paying a few bucks a month will provide a very inefficient DDoS protection, either because they don't have a good one, or because you have to pay for a good protection. Sometimes, a bad protection can even have more negative effects than a little DDoS that you received, filtering useful packages, sometimes, totally blocking UDP traffic. So, chose your server provider carefully, because chances are you'll get DDoSed at some point. However, you can still improve a bad protection with some firewall rules.

### Monitor and DDoS

If your server is set properly, chances are you're running a monitor cronjob.  
The monitor function uses server query to make sure your server is online. But if you're under a DDoS, the server won't be able to answer queries properly, even locally, and the monitor function will detect your server as crashed and will reboot it constantly until the DDoS ends.

For a source server on default port 27015, the following rules will drop anyone who sends more than 10 requests in less than 60 seconds. Those numbers are not mandatory and you're free to adapt them for your needs.

```text
-A INPUT -p udp -m udp --dport 27015 -m state --state NEW -m recent --set --name DEFAULT --rsource
-A INPUT -p udp -m udp --dport 27015 -m state --state NEW -m recent --update --seconds 60 --hitcount 10 --name DEFAULT --rsource -j DROP
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

