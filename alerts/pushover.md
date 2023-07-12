# Pushover

![](../.gitbook/assets/pushover\_logo.png)

[Pushover](https://pushover.net) allows the sending of push notifications to various devices such a PC, phone and tablet. This functionality is used to allow users to receive alerts about LinuxGSM.

## Setup Pushover Alerts

A Pushover application and your user key is required to send messages to Pushover.&#x20;

Visit [here](https://pushover.net/apps/build) to create a new application.

* name: LinuxGSM
* Check the box agreeing to the Terms Of Service.

Once the application has been created get the API key and user key (which can be found in the pushover dashboard).\
Turn on Pushover alerts and paste in API key and user key in the [LinuxGSM config](../configuration/linuxgsm-config.md).

```
# Pushover Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Pushover
pushoveralert="on"
pushoveruserkey="yourpushoverid"
pushovertoken="b5u24t1wua34gmh14kr1s3erkwi7tl"
```
