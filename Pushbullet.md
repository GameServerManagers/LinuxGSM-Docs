<a href="https://www.pushbullet.com"><p align="center"><img src="images/pushbullet/pushbullet_logo.png" alt="Pushbullet logo"/></p></a>
<p align="center">Send LinuxGSM alerts to a Pushbullet user or channel.</p>

<p align="center"><img src="https://linuxgsm.com/wp-content/uploads/2016/05/lgsm-pushbullet.png" alt="Pushbullet alert"/></p>

# Enable Pushbullet alerts
To enable Pushbullet alerts you need to generate an Access Token.

Access Tokens are available from Pushbullet setting found [here](https://www.pushbullet.com/#settings).

Once you have created a token insert it in to you LinuxGSM config.
````bash
# Pushbullet Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Pushbullet
pushbulletalert="on"
pushbullettoken="o.noWN6jpIeBUkLraw24saHKd7ksOkn7on"
channeltag=""
````

# Enable Channels

Alerts can also be sent to Pushbullet channels. Channels are push notification feeds that can be subscribed to. Anything you push to a channel will instantly go to all of the channel's subscribers. Only the owner of a channel can push to it.

Visit [here](https://www.pushbullet.com/my-channel) to generate a channel.

Once you have created the channel set the channeltag in the script without using hash `#`.
```
channeltag="myepicserver"
```

# Send Test Alert
Finally test that is correctly works by sending a test alert.
```
./gameserver test-alert
```