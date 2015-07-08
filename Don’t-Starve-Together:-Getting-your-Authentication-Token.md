# Getting your Authentication Token
You will need Don’t Starve Together installed on your personal computer to get your token.

1. Open up the game on your computer. Once you reach the main menu, press the backtick key (`) on your keyboard. You will see a screen similar to this one:

![DST Terminal](https://github.com/dgibbs64/linuxgsm/blob/master/images/screens/DSTconsole.png)
DST Console.

> note: If you’ve never before played the game, you first need to click on Play and create an account.

2. Copy the following string into the box at the bottom of the console:

`TheNet:GenerateServerToken()`

It should look like this:
![DST Console COmmand](https://github.com/dgibbs64/linuxgsm/blob/master/images/screens/DSTconsolecommand.png) 
DST Console with command

Once you have done this, press **ENTER** on your keyboard. The console will close, and you can exit the game. Locate the file that has been generated in one of the following directories, depending on your operating system.

On Windows, the file is located in:

`%USERPROFILE%/My Documents/Klei/DoNotStarveTogether/server_token.txt`

On Linux:

`~/.klei/DoNotStarveTogether/server_token.txt`

On Mac OS X:
`~/Documents/Klei/DoNotStarveTogether/server_token.txt`

This file is your server token. Do not share it with anyone.

3. Upload the token file to your server.

 `cp server_token.txt ~/.klei/DoNotStarveTogether/`

Original instructions here:

https://www.linode.com/docs/applications/game-servers/dont-starve-together-on-ubuntu#getting-your-authentication-token