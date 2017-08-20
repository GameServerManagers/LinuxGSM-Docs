It is possible to send LinuxGSM alerts to Telegram groups

![Telegram Alert](http://i.imgur.com/iKSfMvf.png)

To do this you will need to setup and Bot and a group.

# Setup a Telegram Bot

To enable Telegram alerts you need to create your own Telegram Bot.

1. Do do this you will need to speak to @BotFather by visiting [here](https://telegram.me/BotFather).

2. Click Send Message to load the @BotFather chat.

3. Click start to begin the chat. 

![BotFather Chat](http://i.imgur.com/BwMsbPp.png)

You will be given a list of available commands for @BotFather

![BotFather Commands](http://i.imgur.com/o6biCLs.png)

4. Type `/newbot` and follow the instructions the create a bot.

![new Bot](http://i.imgur.com/iZwoVk9.png)

5. Once complete an API token will be given. Enter the token to the LinuxGSM config.
```
# Telegram Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Telegram
telegramalert="on"
telegramtoken="401319987:AAGmgLWzYDprqkMHBjCT9qtzIRWCzqgoTLw"
telegramchatid=""

```

# Create a Telegram Group
Once the bot is created it will need to join a group to send alerts. 

1. Select `New Group`

![New Group](http://i.imgur.com/smvfyqR.png)

2. Give your group a name

![Select Bot](http://i.imgur.com/xEEqaWS.png)

3. Select the Bot you just created by typing `@ExampleBot`.

![Add Bot](http://i.imgur.com/8XHgPD1.png)


The bot will now be added to the group.
# Existing group

If you are using an existing group go to View group info>Add Members.

![Add Bot](http://i.imgur.com/8XHgPD1.png)

# Retrieve the chat id

Finally the chat id will be to be retrieved to allow the new bot to send messages to the group.

To obtain the chat id send a message to the new group then visit the following url replacing the `XXXXX` with your bot token from earlier.

```
https://api.telegram.org/botXXXXXXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/getUpdates
```

Look for text similar to the following. That number including the - is the chat id e.g `-191537238`

```
"chat":{"id":-191537238,
```

Add the chat id to the LinuxGSM config

```
# Telegram Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Telegram
telegramalert="on"
telegramtoken="401319987:AAGmgLWzYDprqkMHBjCT9qtzIRWCzqgoTLw"
telegramchatid="-191537238"
```

Now test that is correctly works
```
./gameserver test-alert
```