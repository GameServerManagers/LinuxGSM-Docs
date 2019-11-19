---
description: Allows the selection of specific builds of a game server in SteamCMD
---

# Branch

Game developers sometimes make available several builds of the game server on Steam, often to allow beta testing of new releases. These builds are made available via branches \(betas\) and can be entered in the [LinuxGSM Config](../configuration/linuxgsm-config.md).

## Find Branches

A list of all available branches for a game server are listed on SteamDB under the appid depots.

{% hint style="info" %}
[https://steamdb.info/app/258550/depots/](https://steamdb.info/app/258550/depots/)
{% endhint %}

## Select a Branch

In LinuxGSM is it possible to specify a branch by entering the `branch` setting in the [LinuxGSM Config](../configuration/linuxgsm-config.md).

```text
# Steam App Branch Select
# Example: "latest_experimental"
branch=""
```

