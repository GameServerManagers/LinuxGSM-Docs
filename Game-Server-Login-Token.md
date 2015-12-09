Game Server Login Token is a new system by Valve for managing Game servers.

Generate a token here.
[http://steamcommunity.com/dev/managegameservers](http://steamcommunity.com/dev/managegameservers)

What is the point of GSLT?

To fully understand the reasoning behind GSLTs, we need to back up a bit to July 2015. [Valve announced that running certain plugins would get your server blacklisted](http://dathost.net/blog/important-information-regarding-our-csgo-servers/), meaning it could not connect to the master servers and people wouldn’t be able to connect to the server.

This created a lot of problems for gameserver providers, large communities and anyone providing configurable servers to third parties, as bans were handed out by IP, meaning that an entire machine could be banned because of one malicious or uninformed user.

To address this, Valve is moving the ban to account-level instead of IP-level, which means that the end-user is always responsible for what they run on their server. Of course, gameserver providers and the like still have a responsibility to educate their users on these policies, as some might mistakenly upload blacklisted plugins.

An added benefit is that people who add your server to favorites will still be able to find and connect to your server, even if you change hosting provider and/or the IP / port of your server. This was something that previously was impossible.

Advantages of using GSLT

GSLT creates a persistent token for your game server. This allows any users who have favorited your server to still find your server if you to change your servers IP details. This is very useful if you change your server/hosting provider. Allowing your regular players to easily connect to your new server.

# Currently Supported Servers
Counter-Strike: Global Offensive 
Team Fortress 2 (GSLT not yet required for public servers)

FOr further infomation see this useful blog post: [http://dathost.net/blog/important-information-regarding-our-csgo-servers/](http://dathost.net/blog/important-information-regarding-our-csgo-servers/)