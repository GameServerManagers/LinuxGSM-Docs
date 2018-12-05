---
description: >-
  LAN discovery is required to get Steam based game servers listed in the Steam
  server browser.
---

# LAN Discovery

Many admins who have tried to host LAN servers report issues with LAN game servers now showing up in the LAN tab on the steam server browser 

![LAN Tab on the Steam server browser ](../.gitbook/assets/untitled%20%281%29.png)

## Workarounds

There are two easy workarounds to fix this:

* Connect using the console command

  Syntax: `connect IP:PORT`

  If the port is 27015, then you can just use : `connect IP`

  Examples: `connect 192.168.1.10:27025` ; `connect 192.168.1.10`

* Add the server to the server browser's favourites. If in game, then go to the legacy browser if applicable to find it. The syntax to use is the same as for the console connection.

## Attempt at fixing the issue

As [this github issue](https://github.com/GameServerManagers/LinuxGSM/issues/1770) shows, there might be a possible configuration that fixes the issue, but LinuxGSM devs were not able to reproduce it at the time of writing the doc, so this information is purely experimental. and you are welcome to update it or post on the issue if you have useful information to share about it.

1. Edit your [start parameters](../configuration/start-parameters.md) using your [LinuxGSM config](../configuration/linuxgsm-config.md) files.
2. Change `ip="0.0.0.0"` to an actual interface IP, for example `ip="192.168.1.10"` ; this will allow LinuxGSM to [monitor](../commands/monitor.md) and query your server properly.
3. In the `fn_parms` section, add `+sv_lan 1` and make sure you replace `-ip ${ip}` with `-ip 0.0.0.0`
4. Make sure your server main port listens to one of these IP or IP ranges: `4242, 26900-26905, 27015-27020, 27215`

