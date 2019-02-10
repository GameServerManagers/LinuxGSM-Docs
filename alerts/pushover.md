# Pushover

![](../.gitbook/assets/pushover_logo.png)

Send LinuxGSM alerts to Pushover.

## Setup Pushover Alerts

A Pushover application is required to send messages to Pushover.
1. Visit [here](https://pushover.net/apps/build) to create a new application.

* name: LinuxGSM
* type: Script
* icon:

2. Check the box agreeing to the Terms Of Service.
3. Once the application has been created get the API key.
4. Turn on Pushover alerts and paste in API key and user in the [LinuxGSM config](../configuration/linuxgsm-config.md).

  ```text
  # Pushover Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Pushover
  pushoveralert="on"
  pushoveruserkey="yourpushoverid"
  pushovertoken="b5u24t1wua34gmh14kr1s3erkwi7tl"
  ```
