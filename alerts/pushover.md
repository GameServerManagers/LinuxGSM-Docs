# pushover

[![Pushover logo](https://github.com/GameServerManagers/LinuxGSM-Docs/tree/8e94e0870b2134515a861b85f910435f47d4ae2b/Alerts/images/pushover/pushover_logo.png)](https://pushover.net/)

Send LinuxGSM alerts to Pushover.

## Setup Pushover Alerts

A Pushover application is required to send messages to Pushover. 1. Visit [here](https://pushover.net/apps/build) to create a new application.

* name: LinuxGSM
* type: Script
* icon: 
* check box agreeing to TOS
* Once the application has been created get the API key.
* Turn on Pushover alerts and paste in API key and user in the LinuxGSM config.

  ```text
  # Pushover Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Pushover
  pushoveralert="on"
  pushoveruserkey="yourpushoverid"
  pushovertoken="b5u24t1wua34gmh14kr1s3erkwi7tl"
  ```

