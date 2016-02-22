This WILL help you on the making of a new server support for LGSM.

Can be a good start to copy your main script from an existing game (preferably the same engine if it exists).

Things to edit into the main script : 
* Check paths variables, especially config paths
* appid="" (steamcmd games only)
* servicename=""
* gamename=""
* engine=""


Functions to check and change if needed

* command_install.sh
* install_config.sh
* command_monitor.sh & monitor_gsquery.sh & gsquery.py (in GameServerQuery)
* command_details.sh


