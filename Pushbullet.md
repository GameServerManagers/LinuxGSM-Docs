Pushbullet alerts allow you to recieve messages if your monitored server goes down is restarted or updated (See [[Monitor]]).

![](https://gameservermanagers.com/wp-content/uploads/2016/05/lgsm-pushbullet.png)

# Enable alerts
To enable Pushbullet alerts you will need to edit the gameserver script.

Generate your access token here: https://www.pushbullet.com/#settings

```
# Pushbullet Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Pushbullet
pushbulletalert="on"
pushbullettoken="o.noWN6jpIeBUkLraw24saHKd7ksOkn7on"
```
# Enable Channels

> note: leave blank if not in use

It is now possible to push to channels as well. Channels are push notifications feeds that can be subscribed to. Anything you push to a channel will instantly go to all of the channel's subscribers. Only the owner of a channel can push to it.

Generate a channel here: https://www.pushbullet.com/my-channel

Once you have created the access channel set in the script without using hash `#`. 
e.g `channeltag="myepicserver"` would push to `#myepicserver`
```
channeltag=""
```

You can test the alert feature using `test-alert`
````bash
./gameserver test-alert
````