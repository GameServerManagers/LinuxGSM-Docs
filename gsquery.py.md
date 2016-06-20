## What is gsquery ?

## How to use

Simply use the [[Monitor]] function, and if gsquery is present, it will be used.


### Current state of GSM

Currently gsquery ships with the GSM install.


### Older released of GSM

The [gsquery addon](https://gameservermanagers.com/dl/gsquery.py) is suggested when installing your game server. It provides a more reliable way to [[Monitor]] your server by querying it, instead of just checking if the server process is down. Said another way, it allows LGSM to detect a frozen server that nobody could join anymore and reboot it automatically.

## "I answered no to gsquery, and now i want it !"

Just `cd` to your main script directory and run those two commands : 

    wget https://gameservermanagers.com/dl/gsquery.py
    chmod +x gsquery.py

Done.


### Known issue
The only known limit noted to this function has been seen in Garry's Mod, where the server would sometimes be frozen, but still answer to queries.