---
description: How LinuxGSM handles IP addresses
---

# IP Address Configuration

{% hint style="info" %}
Make sure you understand basic [IP addressing](../networking/ip-address.md).
{% endhint %}

By default, LinuxGSM will use the [0.0.0.0](../networking/ip-address.md#0.0.0.0) meta-address. This behavior will allow the game server to bind to **all** interfaces and allow LinuxGSM to [quer](../commands/monitor.md)[y](../commands/monitor.md) all available IP addresses. If there are multiple IP addresses available, [details](../commands/details.md) will display 0.0.0.0.&#x20;

Internet IP: LinuxGSM will try to gather the server's internet IP address to be shown in [details](../commands/details.md).

Specific IP: If a specific IP address needs to be set it can be done using the `ip` setting in the [LinuxGSM](linuxgsm-config.md) or [game server config](game-server-config.md) files. Depending upon the game server this will allow it to _bind_ to a specific IP address.

Display IP: If you want to change the IP address displayed in _alerts_ you can use the [displayip](../alerts/#display-ip).
