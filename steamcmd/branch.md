---
description: Allows the selection of specific builds of a game server in SteamCMD
---

# Branch

Game developers sometimes make available several builds of the game server on Steam, often to allow beta testing of new releases. These builds are made available via _branches \(betas\)_ and can be entered in the [LinuxGSM Config](../configuration/linuxgsm-config.md).

## Find Branches

A list of all available branches for a game server are listed on SteamDB under the appid depots.

{% hint style="info" %}
[https://steamdb.info/app/258550/depots/](https://steamdb.info/app/258550/depots/)
{% endhint %}

## Select a Branch

The default SteamCMD branch is `public`. However, it is possible to use other builds by entering a branch name in the `branch` setting in your [LinuxGSM config](../configuration/linuxgsm-config.md). 

```text
# Steam App Branch Select
# Example: "latest_experimental"
branch="staging"
```

## Beta Password

Some branches require a password. This can be done by entering a password in the`betapassword` setting in your [LinuxGSM config](../configuration/linuxgsm-config.md).

```text
betapassword="branchpassword"
```

