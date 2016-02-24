This may help you on the making of a new server support for LGSM.

First, it can be a good start to copy a main script from an existing game (preferably the same engine if it exists) and edit it to fit your needs.

Things to edit into the main script : 
* Check paths variables, especially config paths
* appid="" (steamcmd games only)
* servicename=""
* gamename=""
* engine=""
* githubuser/repo/branch="" (if you dev on your own github or a branch can help a lot)

Functions to check and change if needed

* command_install.sh
* install_config.sh
* command_monitor.sh & monitor_gsquery.sh & gsquery.py (in GameServerQuery)
* command_details.sh


