# Automation with cronjobs
You can set scheduled tasks with cronjobs, to run any function at any given time.  

Most used ones are:
- Automatically check for updates (update command)
- Automatically check for server crash and restart if needed (monitor command)
- Automatically keep LGSM up to date (update-functions command)
- Automatically restart the server at a given time (restart command)
- Automatically update and restart the server (force-update command)

LGSM team advise you to use root cronjobs to manage everything in one place. Just login as root, then edit your cronjobs. 

## Command
To access and edit your cronjobs, input  
`crontab -e`

You may be prompted for choosing a text editor the first time.  
If you with to change crontab's text editor, you can run:   
`export EDITOR=vim` or `export EDITOR=nano`

## Daily cronjobs

**Replace the username and gameserver according to your case**

Here is an example of a user based cronjob for daily restart at 5am : 

````bash
0 5 * * *  /home/username/gameserver restart > /dev/null 2>&1
````

Here is an example of a root based cronjob for daily restart at 5am : 

````bash
0 5 * * *  su - username -c '/home/username/gameserver restart' > /dev/null 2>&1
````

## Every x time cronjobs

**Replace the username and gameserver according to your case**

Here is an example of a user based cronjob to monitor your server every 3 minutes : 

````bash
*/3 * * * *  /home/username/gameserver monitor > /dev/null 2>&1
````

Here is an example of a root based cronjob to monitor your server every 3 minutes : 
````bash
*/3 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
````


# Full examples

## Complete setup for one gameserver

**Replace the username and gameserver according to your case**

````bash
####CRONJOBS####

### Game Name
#Server Name
*/5 * * * * su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1
*/30 * * * * su - username -c '/home/username/gameserver update' > /dev/null 2>&1
30 6 * * *  su - username -c '/home/username/gameserver force-update' > /dev/null 2>&1
0 0 * * 0 su - username -c '/home/username/gameserver update-functions' > /dev/null 2>&1
````

* Will monitor your server every 5 minutes
* Will check for an update every 30 minutes, update and restart only if an update is detected.
* Will restart and check for an update every day at 6:30 AM
* Will update your LGSM functions every Sunday at midnight.

### Real life multiple servers example

````bash
####CRONJOBS####

###TeamSpeak###
# TS3Community
*/1 * * * *  su - ts3server -c '/home/ts3server/ts3server monitor' > /dev/null 2>&1
30 6 * * *  su - ts3server -c '/home/ts3server/ts3server update' > /dev/null 2>&1
0 0 * * 0 su - ts3server -c '/home/ts3server/ts3server uf' > /dev/null 2>&1

###GMOD###
# ProBuild
*/2 * * * *  su - gmodprobuild -c '/home/gmodprobuild/gmodserver monitor' > /dev/null 2>&1
0 5 * * *  su - gmodprobuild -c '/home/gmodprobuild/gmodserver fu' > /dev/null 2>&1
0 0 * * 0 su - gmodprobuild -c '/home/gmodprobuild/gmodserver uf' > /dev/null 2>&1
# Prophunt
*/2 * * * *  su - gmodprophunt -c '/home/gmodprophunt/gmodserver monitor' > /dev/null 2>&1
0 5 * * *  su - gmodprophunt -c '/home/gmodprophunt/gmodserver fu' > /dev/null 2>&1
0 0 * * 0 su - gmodprophunt -c '/home/gmodprophunt/gmodserver uf' > /dev/null 2>&1


###CSS###
# GunGame
*/2 * * * *  su - cssgungame -c '/home/cssgungame/cssserver monitor' > /dev/null 2>&1
30 5 * * *  su - cssgungame -c '/home/cssgungame/cssserver fu' > /dev/null 2>&1
0 0 * * 0 su - cssgungame -c '/home/cssgungame/cssserver uf' > /dev/null 2>&1

###RUST###
# Modded
## Server stopped
#*/5 * * * * su - rustmodded -c '/home/rustmodded/rustserver monitor' > /dev/null 2>&1
#30 6 * * *  su - rustmodded -c '/home/rustmodded/zip-updater/zip-updater' > /dev/null 2>&1
#0 0 * * 0 su - rustmodded -c '/home/rustmodded/rustserver uf' > /dev/null 2>&1

#Vanilla
*/5 * * * * su - rustvanilla -c '/home/rustvanilla/rustserver monitor' > /dev/null 2>&1
*/30 * * * * su - rustvanilla -c '/home/rustvanilla/rustserver update' > /dev/null 2>&1
30 6 * * *  su - rustvanilla -c '/home/rustvanilla/rustserver fu' > /dev/null 2>&1
0 0 * * 0 su - rustvanilla -c '/home/rustvanilla/rustserver uf' > /dev/null 2>&1

###ARK###
*/30 * * * * su - arkserver -c '/home/arkserver/arkserver monitor' > /dev/null 2>&1
0 6 * * 5  su - arkserver -c '/home/arkserver/arkserver fu' > /dev/null 2>&1
0 */1 * * * su - arkserver -c '/home/arkserver/arkserver update' > /dev/null 2>&1
0 0 * * 0 su - arkserver -c '/home/arkserver/arkserver uf' > /dev/null 2>&1
````

#### Protips
* Note the "fu" (for "force-update") which will check for an update and restart your server even though there is no update. It is a good alternative if you don't wish to use the updateonstart functionality.
* It's a good practice to comment cronjob lines of a server that you momentarily want to shutdown in order to add back cronjobs more easily afterwards.
* Some servers crash more often, so it's a good idea to monitor them more frequently. However, you shouldn't monitor faster than once every 2 minutes, otherwise the monitor function might behave inconsistently, and your server might bootloop.
* You can also sparingly run "every x time" update checks, for games getting updated a lot.
* As you can see for the commented Rust server, you can also run your own custom scripts if the task is more complicated than just an LGSM command.
* Ultimately, it's wise to add an "uf" cronjob (for "update-functions") in order to keep LGSM up to date.

# Cronjobs generalities

### Syntax

#### User cronjobs
````bash
* * * * * [/path/to/script] [command]  > /dev/null 2>&1
````

#### Root cronjobs
````bash
* * * * * [/path/to/script] [command]  > /dev/null 2>&1
````

**Note**: The ` >/dev/null 2>&1` is required to mute the execution (don't save or send output)

### Temporal values 
`*` can be considered as "bypass" values.  
You can replace them by numerical values standing for  
**minutes** - **hours** (24h format) - **days** - **month** - **day of the week** (Sunday =0 to Saturday =6)


#### Every "x" time
In order to run a command, such as "monitor" every "x" time, there is a simple solution.  
Replace `*` by `*/x`, "x" being the desired numerical value.  
Think about defining smaller amounts of time to a fixed value when using this. For example, if you wish to have an "every two hours" cronjob, you'll need to set a fixed value for minutes.

#### Temporal values examples
Every single minute    
`* * * * *`

Every 30 minutes  
`*/30 * * * *`

Every hour  
`0 * * * *`

Every two hours  
`0 */2 * * *`

Every day at 5:10 PM  
`10 17 * * *`

Every Wednesday at 1 AM   
`* 1 * * * 3`

Every five days at 1 AM  
`* 1 */5 * *`

### Cronjob generator

If you have any doubt about a particular syntax, you can use this generator : http://crontab-generator.org/