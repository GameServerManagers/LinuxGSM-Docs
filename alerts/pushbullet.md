# Pushbullet

![](../.gitbook/assets/pushbullet_logo%20%281%29.png)

[Pushbullet](https://www.pushbullet.com) allows the sending of push notifications to various devices such a PC, phone and tablet. This functionality is used to allow users to recieve alerts about LinuxGSM.

## Enable Pushbullet alerts

To enable Pushbullet alerts an _Access Token_ needs to be generated. Access Tokens are available from Pushbullet setting found [here](https://www.pushbullet.com/#settings).

Once you have created a token insert it in to you [LinuxGSM config](../configuration/linuxgsm-config.md).

```bash
# Pushbullet Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Pushbullet
pushbulletalert="on"
pushbullettoken="o.noWN6jpIeBUkLraw24saHKd7ksOkn7on"
channeltag=""
```

## Enable Channels

Alerts can also be sent to Pushbullet channels. Channels are push notification feeds that can be subscribed to. Anything you push to a channel will instantly go to all of the channel's subscribers. Only the owner of a channel can push to it.

Visit [here](https://www.pushbullet.com/my-channel) to generate a channel.

Once you have created the channel set the channeltag in the script without using hash `#`.

```text
channeltag="myepicserver"
```

