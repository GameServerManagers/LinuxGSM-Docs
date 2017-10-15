<a href="https://pushover.net/"><p align="center"><img src="images/pushover/pushover_logo.png" alt="Pushover logo"/></a>
<p align="center">Send LinuxGSM alerts to Pushover.</p>

# Setup Pushover Alerts
A Pushover application is required to send messages to Pushover.
1. Visit [here](https://pushover.net/apps/build) to create a new application.
* name: LinuxGSM
* type: Script
* icon: 
* check box agreeing to TOS

2. Once the application has been created get the API key.

3. Turn on Pushover alerts and paste in API key in the LinuxGSM config.
```
# Pushover Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Pushover
pushoveralert="on"
pushoveruserkey="yourpuhoverid"
pushovertoken="b5u24t1wua34gmh14kr1s3erkwi7tl"
```