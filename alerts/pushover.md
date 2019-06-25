# Pushover

![](../.gitbook/assets/pushover_logo.png)

[Pushover](https://pushover.net) allows the sending of push notifications to various devices such a PC, phone and tablet. This functionality is used to allow users to recieve alerts about LinuxGSM.

## Setup Pushover Alerts

A Pushover application is required to send messages to Pushover. 1. Visit [here](https://pushover.net/apps/build) to create a new application.

* name: LinuxGSM
* type: Script
* icon:
* Check the box agreeing to the Terms Of Service.
* Once the application has been created get the API key.
* Turn on Pushover alerts and paste in API key and user in the [LinuxGSM config](../configuration/linuxgsm-config.md).

  ```text
  # Pushover Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Pushover
  pushoveralert="on"
  pushoveruserkey="yourpushoverid"
  pushovertoken="b5u24t1wua34gmh14kr1s3erkwi7tl"
  ```

