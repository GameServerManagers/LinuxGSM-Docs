Getting your Authentication Token
You will need Don’t Starve Together installed on your personal computer to get your token.

Open up the game on your computer. Once you reach the main menu, press the backtick key (`) on your keyboard. You will see a screen similar to this one:

DST Console.

If you’ve never before played the game, you first need to click on Play and create an account.
Copy the following string into the box at the bottom of the console:

1
TheNet:GenerateServerToken()
It should look like this: DST Console with command

Once you have done this, press ENTER on your keyboard. The console will close, and you can exit the game. Locate the file that has been generated in one of the following directories, depending on your operating system.

On Windows, the file is located in:

1
%USERPROFILE%/My Documents/Klei/DoNotStarveTogether/server_token.txt
On Linux:

1
~/.klei/DoNotStarveTogether/server_token.txt
On Mac OS X:

1
~/Documents/Klei/DoNotStarveTogether/server_token.txt
This file is your server token. Do not share it with anyone.
Upload the token file to your Linode. If you’re running OS X or Linux, you can use the following command, replacing your IP address and username:

1
 scp ~/Documents/Klei/DoNotStarveTogether/server_token.txt user@12.34.56.78:~/.klei/DoNotStarveTogether/


https://www.linode.com/docs/applications/game-servers/dont-starve-together-on-ubuntu#getting-your-authentication-token