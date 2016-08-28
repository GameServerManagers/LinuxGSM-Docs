# What are firewalls ?

Firewalls are part of a very complex topic, but let's try to sum up their purposes, usages, and limits.

The main idea is to prevent certain kind of connections to happen, whether it's incoming our outgoing, IP and port restriction, or requests quotas. The goal is to protect against some sorts of hacking and DDoS. However the main downside is that unless you're using a very restrictive firewall, you'll probably waste more time than protect yourself against anything. For example, say you disallow any incoming connection to everything that isn't important, and leave everything important open to any IP without any restrictions (which is a common practice), then you just wasted your time. In this case, you'd better make sure that what's listening is secured and "voilà". If your server gets popular, chances are some people will try to shutdown your services using DDoS. If your server provider doesn't have an efficient DDoS protection, a good practice is to drop their packets to prevent your services from being shut down. There are some good practices that might help getting your servers more reliable. Here are some of them. 


# iptables

[iptables](http://ipset.netfilter.org/iptables.man.html)is the most used and supported Linux firewall. You'll find plenty of documentations all over the web. Firewall settings usually gets reset on a reboot, which is a good thing, because if you mess around you can still reboot. People use to make very basic scripts to apply the firewall settings back easily, and eventually start it on server boot. But protip: Whatever you do, make sure to test a firewall setting before setting it on boot, because you might make an error preventing you from connecting back to your machine... Don't laugh, i'm pretty sure it's not a legend, it might happen to you.


## DDoS protection

### Monitor and DDoS
If your server is set properly, chances are you're running a monitor cronjob.  
Well, the monitor function uses server query to make sure your server is online. But if you're under a DDoS, the server won't be able to answer queries properly, even locally, and the monitor function will detect your server as crashed and will reboot it constantly.

````
-A INPUT -p udp -m udp --dport 27015 -m state --state NEW -m recent --set --name DEFAULT --rsource
-A INPUT -p udp -m udp --dport 27015 -m state --state NEW -m recent --update --seconds 60 --hitcount 10 --name DEFAULT --rsource -j DROP
````

This will drop anyone who sends more than 10 requests in less than 60 seconds. Those numbers are not mandatory and you're free to adapt them for your needs.