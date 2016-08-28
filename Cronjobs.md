# Automation with cronjobs
You can set scheduled tasks with cronjobs, to run any function at any given time.
LGSM team advise you to use root cronjobs to manage everything in one place. Just login as root, then edit your cronjobs. 

To edit your cronjobs, type : 

`crontab -e`


## Daily cronjobs

**Replace the username and gameserver according to your case**

Here is an example of a user based cronjob for daily restart at 5am : 

`0 5 * * *  /home/username/gameserver restart > /dev/null 2>&1`

Here is an example of a root based cronjob for daily restart at 5am : 

`0 5 * * *  su - username -c '/home/username/gameserver restart' > /dev/null 2>&1`

## Every x time cronjobs

**Replace the username and gameserver according to your case**

Here is an example of a user based cronjob to monitor your server every 3 minutes : 

`*/3 * * * *  /home/username/gameserver monitor > /dev/null 2>&1`

Here is an example of a root based cronjob to monitor your server every 3 minutes : 
`*/3 * * * *  su - username -c '/home/username/gameserver monitor' > /dev/null 2>&1`


## Syntax

### Temporal values 
Each `*` is a bypassed temporal value, that you can replace by an actual value. They are placed in that order : 

minutes - hours - days - month - day of the week (sunday =0, saturday =6)

The true meaning of `*` is : "every single minute/hour/day...", but you can understand it as "i don't care of this value". If you replace one `*` by a number, then it will take care of it. If instead you're using `*/x`, it then means : every "x" time.

For example, every single minute will be : `* * * * *`

Every day at 5:10 AM will be : `10 5 * * *`

And every hour and 10 minutes will be : `*/10 */1 * * *`

### /dev/null 2>&1
The ` >/dev/null 2>&1` means that it will mute the execution (don't save or send output)

## Example of a cron setup
````
0       0       *       *       0       su - nmrihserver -c '/home/nmrihserver/nmrihserver1 update-functions' > /dev/null 2>&1
0       *       *       *       *       su - nmrihserver -c '/home/nmrihserver/nmrihserver1 update' > /dev/null 2>&1
0       *       *       *       *       su - nmrihserver -c '/home/nmrihserver/nmrihserver2 update' > /dev/null 2>&1
0       *       *       *       *       su - nmrihserver -c '/home/nmrihserver/nmrihserver3 update' > /dev/null 2>&1

*/5     *       *       *       *       su - nmrihserver -c '/home/nmrihserver/nmrihserver1 monitor' > /dev/null 2>&1
*/5     *       *       *       *       su - nmrihserver -c '/home/nmrihserver/nmrihserver2 monitor' > /dev/null 2>&1
*/5     *       *       *       *       su - nmrihserver -c '/home/nmrihserver/nmrihserver3 monitor' > /dev/null 2>&1
````

This example updates LGSM functions once per week on sunday, checks for updates once per hour and runs monitor every 5 mins.