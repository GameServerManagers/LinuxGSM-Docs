Here are the Dont Starve Together install guides. A Linux one is included. There is a step within the guide about Authentication Tokens.
http://steamcommunity.com/id/ToNiO44/myworkshopfiles/?section=guides&appid=322330

# The Below instructions are out of date.
For further info on DST Dedicated servers visit this wiki http://dont-starve-game.wikia.com/wiki/Guides/Don%E2%80%99t_Starve_Together_Dedicated_Servers

# Getting your Authentication Token

1. Start Don't Starve Together from Steam and click on the "Play!" button.

![DST Title](images/dst/DST_title.png)

2. Click on the "Acct Info" button.

![DST Menu](images/dst/DST_menu.png)

3. Click on the "Generate Server Token" button, copy the token, and paste it into the file:

~/.klei/DoNotStarveTogether/MyDediServer/cluster_token.txt 

You can quickly do this by running the following command, replacing YourServerTokenHere with your server token (Keep the quotes around the token).

echo 'YourServerTokenHere' > ~/.klei/DoNotStarveTogether/MyDediServer/cluster_token.txt
 

***
OLD INSTRUCTIONS

1: Open up the game on your computer. Once you reach the main menu, press the backtick key (`) on your keyboard. You will see a screen similar to this one:

![DST Terminal](images/dst/DSTconsole.png)
DST Console.

> note: If you’ve never before played the game, you first need to click on Play and create an account.

2: Copy the following string into the box at the bottom of the console:

`TheNet:GenerateServerToken()`

It should look like this:
![DST Console Command](images/dst/DSTconsolecommand.png) 
DST Console with command

Once you have done this, press **ENTER** on your keyboard. The console will close, and you can exit the game. Locate the file that has been generated in one of the following directories, depending on your operating system.

On Windows, the file is located in:

`%USERPROFILE%/My Documents/Klei/DoNotStarveTogether/server_token.txt`

On Linux:

`~/.klei/DoNotStarveTogether/server_token.txt`

On Mac OS X:
`~/Documents/Klei/DoNotStarveTogether/server_token.txt`

This file is your server token. Do not share it with anyone.

3: Upload the token file to your server.

 `cp server_token.txt ~/.klei/DoNotStarveTogether/`

Original instructions here:

https://www.linode.com/docs/applications/game-servers/dont-starve-together-on-ubuntu#getting-your-authentication-token