---
description: Some game servers are listed on the steam master server list
---

# Steam Master Server

For a game server to be seen online it normally has to register itself on a master server list. Valve maintains a master server for many different games. The master server is used to populate the server browser.

![](../.gitbook/assets/screenshot-from-2019-06-09-23-48-11.png)

## Master Server Check

LinuxGSM can check that supported game servers are listed on the steam master server. This is useful for confirming that the server is actually registering and to help diagnose issues.

You can check that your server is listed on the master server by using `./gameserver details`&#x20;

```
Master server:    listed
```

{% hint style="info" %}
Not all game servers support this option but if it does the setting is set to true by default.&#x20;
{% endhint %}

```
steammaster="true"
```

## Troubleshooting: Server Missing from Master Server List

There are instances when a game server might not appear in the server list due to several common reasons:

* Server Loading Time: Please be patient while the server loads, as it may take some time before it becomes visible. Depending on the game server type, certain servers require additional time for tasks like map seeding or loading mods.
* Blocked or Misconfigured [Ports](../networking/ports.md): Ensure that the ports are correctly set up and not blocked. To verify the connection, try connecting directly to the server.
* Filtering in Server List: Check that you have not applied any filters in the server browser. Filters like specific maps, "Empty Server," or "Password Protected" should be unchecked to display all available servers.
* Server Browser Limitations: It's possible that the server browser functionality of the game might not list all available game servers. In such cases, not all servers may be visible in the server list.
