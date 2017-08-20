![Telegram Logo](https://telegram.org/img/t_logo.png)

 send alerts to Telegram

![Telegram Alert](http://i.imgur.com/iKSfMvf.png)

# Enable Telegram Alerts

To enable Telegram alerts you need to create your own Telegram Bot.

Do do this you will need to speak to @BotFather

https://telegram.me/BotFather

Click Send Message to load the @BotFather chat

![BotFather page](http://i.imgur.com/ilsow1W.png)

Click start to begin the chat.

![BotFather Chat](http://i.imgur.com/BwMsbPp.png)

You will be given a list of available commands for @BotFather



![BotFather Commands](http://i.imgur.com/o6biCLs.png)

Type `/newbot` and follow the instructions. Once complete you will have a new bot created
![new Bot](http://i.imgur.com/iZwoVk9.png)

You will now have an API key for your bot. Enter this in to the LinuxGSM config (common.cfg etc).
![LinuxGSM Telegram Settings](http://i.imgur.com/7KGvr35.png)

Now the bot will need to join a group to send messages. If you already have a group skip this step

![New Group](http://i.imgur.com/smvfyqR.png)

Give your group a name

![Select Bot](http://i.imgur.com/xEEqaWS.png)

Next select the Bot you just created by typing @ExampleBot.
If you are using an existing group go to View group info>Add Members 

![](http://i.imgur.com/8XHgPD1.png)

The bot will now be added to the group.

Finally the chat ID will be to be retrieved to allow the new bot to send messages to it.

To obtain the chat ID send a message to the new group then visit the following url replacing the XXXXX with your bot token from earlier.
```
https://api.telegram.org/botXXXXXXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/getUpdates
```

Look for text similar to the following. That number including the - is the chat id e.g `-191537238`

```
"chat":{"id":-191537238,
```

Add the chat ID to the LinuxGSM config

![LinuxGSM telegram Chat ID](http://i.imgur.com/x8pbEA5.png)


Now test that is correctly works
```
./gameserver test-alert
```