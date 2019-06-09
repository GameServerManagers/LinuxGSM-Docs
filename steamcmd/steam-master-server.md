---
description: Some game servers are listed on the steam master server list
---

# Steam Master Server

For a game server to be seen online it normally has to register itself on a master server list. Valve maintains a master server for many different games. The master server is used to populate the server browser.

![](../.gitbook/assets/screenshot-from-2019-06-09-23-48-11.png)

## Master Server Check

LinuxGSM can check that supported game servers are listed on the steam master server. This is useful for confirming that the server is actually registering and to help diagnose issues.

{% hint style="info" %}
Not all game servers support this option but if it does the setting is set to true by default. 
{% endhint %}

```text
steammaster="true"
```

