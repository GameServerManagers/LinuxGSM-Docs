# Using server console

Most game servers offers a console, in which you can monitor activity of your server, check errors in real time, and input some commands.

**IMPORTANT NOTE** : Replace **gameserver** by your actual script name, for example : **csgoserver** or **ts3server**

## Accessing the console

Run the following command : 

`./gameserver console`

Answer **y** to the promp, and voilà !



## Exiting the console properly

To exit the console and let the server running, two steps : 

Press **CTRL + b**, then, press **d**

Note : This shortcut is inherent to [TMUX that LGSM is using](https://github.com/dgibbs64/linuxgsm/wiki/Tmux).



## Exiting the console and shutdown the server with a barbarian method

To force close the server instantly your server while being into the console : 

Press **CTRL + c** 

Note that this doesn't remove the lockfile, so if a monitor cronjob is running it will still auto-restart the server.



## Reminder

### To shutdown your server properly while being into the console :
 
Exit the console with **CTRL + b**, then, press **d**

Then simply run : 

`./gameserver stop`