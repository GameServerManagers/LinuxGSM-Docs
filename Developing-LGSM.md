This page has been designed to help you learn how LGSM code works.

As a user, it will allow you for a better understanding of LGSM and a better administration.  
As a developer, it will help you adding new servers for LGSM, adding functionalities and fixing bugs.

# Generalities

LGSM's "gameserver" script is important but isn't the core script at all. The point is to keep it as simple as possible for users to be able to edit it (settings are located in this file) but get most actual functions into script files so that users can update them with `gameserver update-functions`. Most script routines are done through those functions. Some are global ones for all LGSM servers, while some others are a little more specific. Some checks are based on the "gamename", some others on the "engine". We will get through most of that into this guide.

## Main script (gameserver)

Main scripts need to be clear and simple enough for users to edit them. They have several goals: 
* Provide information about the scripts through comments into the header
* Prevent starting as root (for safety and common sense reasons)
* Set directories variables
* Set Github repo and branch
* Set LGSM preferences through variables
* Set server's startup variables used in `fn_parms `and `parms=""`
* Download LGSM core files (fn_fetch_core_dl)

### Directories
All working directories are set through variables.
* ${rootdir} | Directory containing the "gameserver" main script file
* |_ ${lgsm} directory contains
* |_____________________________ ${functionsdir} | functions | LGSM functions
* |_____________________________ ${libdir} | lib | Library files for fixes (glibc and so on)
* |_____________________________ ${tmpdir} | tmp | Temporary directory
* |_ ${filesidr} | serverfiles | Contains actual server files
* |_ ${backupdir} | backups | Contains server files backups if created
* |_ ${scriptlogdir} | "${rootdir}/log/script" | Contains LGSM logs
* |_ ${consolelogdir} | "${rootdir}/log/console" | Contains TMUX (console output) logs

Developers note: you will need to have a closer look at `## Server Specific Directories`

### Server specific information

Here are the things you need to look after when deploying a new server:

* `## SteamCMD Login` section needs to be present only if the game server requires a steam connection.
* Paths variables, especially config paths
* appid="" (steamcmd games only)
* servicename="" (must be unique)
* gamename="" (must be unique)
* engine=""
* githubuser/repo/branch="" (if you dev on your own github or a branch can help a lot)

### Server Settings and start command

This part contains any setting that can be set as a start command for the given server.
You will then use `fn_parms` and its `parms=""` variable to call those start parameters.

## Functions, commands and script files

Script files are located in ${functionsdir}, which is ${rootdir}/lgsm/functions

* Every single script file must be declared in core_functions.sh
* Commands are declared in core_getopt.sh, depending on the game or engine

Note: You need to update those files with update-functions command after adding a new one.

## Commands

Here are the command functions you might need to alter when adding a new server:
* command_install.sh - Server installation must work properly
* command_update.sh - if the given game supports updates (might required to add a file for that matter, for now, we use to add a single file for install and update, like for TeamSpeak 3).
* command_details.sh - Server details need to be displayed properly
* command_monitor.sh & monitor_gsquery.sh, gsquery.py & gsquery.py - You'll need to read carefully and understand this code before altering it.
* core_getopt.sh - You will define available commands in this one, displayed when the user runs `./gameserver` without an argument. Either use an existing opt or make a new one if needed.
* command_start.sh & command_stop.sh - Of course, your server needs to be able to start and stop properly.
* command_debug.sh & command_console.sh - Those commands usually work out of the box, but might require some more work. If not using tmux, then console should be disabled for this server in core_getopt.sh.

## Fixes

`command_install.sh` runs `fix.sh` at the end of server installation. If the given server requires a fix, then add `fix_gameserver.sh` and run it from `fix.sh`.

## Core functions

### core_dl.sh
This is the first script to be run when `gameserver `is executed.
This script allows for fetching LGSM core files, but also for downloading big files within kind of an API.

### core_functions.sh
This is the second script to be run when `gameserver `is executed.
This script declares all functions and fetches them when they are required.

### core_getopt.sh
This is the third and last script to be run when `gameserver `is executed.
This script allows for setting and printing available commands to the user.

### core_messages.sh
This script allows for easy message output and logging. More details about it in the next part.

## Messages & Logs

LGSM has a message/logging framework to avoid painful syntax into scripts.

Framework syntax is: `fn_print_whatever "This is your message"`
If you want to replace the line afterwards, then reuse `fn_print_whatever`. If you want a new output on a new line, then use `fn_print_whatever_nl`. "nl" stands for "new line".


### On-Screen - Automated functions
* [ .... ] | fn_print_dots | fn_print_dots_nl
* [  OK  ] | fn_print_ok | fn_print_ok_nl
* [ FAIL ] | fn_print_fail | fn_print_fail_nl
* [ ERROR ] | fn_print_error | fn_print_error_nl
* [ WARN ] | fn_print_warn | fn_print_warn_nl
* [ INFO ] | fn_print_info | fn_print_info_nl

### On-Screen - Interactive messages
* Print $gamename $commandaction and jump some lines | fn_print_header (used at the beginning of a command)
* Complete! |fn_print_complete | fn_print_complete_nl
* Failure! | fn_print_failure | fn_print_failure_nl
* Error! | fn_print_error2 | fn_print_error2_nl
* Warning! | fn_print_warning | fn_print_warning_nl
* Information! | fn_print_information | fn_print_information_nl

### On-Screen End of Line
* OK| fn_print_ok_eol | fn_print_ok_eol_nl
* FAIL | fn_print_fail_eol | fn_print_fail_eol_nl
* WARN | fn_print_warn_eol | fn_print_warn_eol_nl
* FAIL | fn_print_info_eol | fn_print_info_eol_nl
* QUERYING | fn_print_querying_eol | fn_print_querying_eol_nl
* CHECKING | fn_print_checking_eol | fn_print_checking_eol_nl
* CANCELED | fn_print_canceled_eol | fn_print_canceled_eol_nl
* REMOVED | fn_print_removed_eol | fn_print_removed_eol_nl
* UPDATE | fn_print_update_eol | fn_print_update_eol_nl

### Logging
Syntax: `fn_script_log "Message goes here."`  
Output: `## Feb 28 14:56:58 ut99-server: Monitor: Message goes here.`

* Simple action log | fn_script_log 
* PASS (a successful test) | fn_script_log_pass
* FATAL (an error has interrupted LGSM) | fn_script_log_fatal
* ERROR | fn_script_log_error
* WARN | fn_script_log_warn
* INFO | fn_script_log_info

## Checks

Any script file must run `check.sh` at some point.  
Within `check.sh`, you will then chose what tests to run for a given function. The syntax of check.sh is a bit counter intuitive: `local allowed_commands_array=( )` is the variable where you will enter the functions into which you need to run the following check.

There are several checks available:
* check_config.sh checks for a missing config file or a wrong parameter.
* check_deps.sh checks for missing dependencies and contains requirements
* check_glibs.sh checks if the server has the correct Glibc version or a fix available.
* check_ip.sh automatically identifies the server interface IP.
* check_logs.sh checks if log files exist.
* check_permissions.sh checks ownership & permissions of scripts, files and directories
* check_root.sh checks if the user tried to run the script as root
* check_status.sh checks the process status of the server. Either online or offline
* check_steamcmd.sh checks if SteamCMD is installed correctly
* check_system_dir.sh checks if systemdir is accessible
* check_system_requirements.sh checks RAM requirements (maybe more into the future)
* check_tmuxception.sh checks and prevents server start from tmux or screen

### core_exit.sh 
This script allows for the use of exit codes which will print different outputs to LGSM logs.
Running `core_exit.sh` defaults exitcode variable to 0 which stands for a proper exit
* Normal exit: exitcode=0
* FATAL  exitcode=1
* ERROR: exitcode=2
* WARN: exitcode=3

## Server installation

Installing a new server is mainly done through two scripts:

* install_server_files.sh
* install_config.sh

Sometimes, another script is required, such as for TeamSpeak 3: `update_ts3.sh`

## Versioning

At the moment, only the main "gameserver" script has a version number.
Syntax is pretty easy, it's all incremental, based on the date:
`version="YYMMDD"`


# Testing and debugging your code

## Working from your own github branch

You will usually be developing onto your own repo. Using your own repo instead of the original one is quite easy.

1. Display your main "gameserver" file on github, and select "Raw".
2. Make a test user, login to it
3. wget your Raw link and chmod +x the script.
4. Edit your "gameserver" file by changing github information to your username and repo and branch.
````bash
## Github Branch Select
# Allows for the use of different function files
# from a different repo and/or branch.
githubuser="YourUsername"
githubrepo="YourRepository"
githubbranch="YourBranchName"
````

Now, any command you run will get your own github files, and after any change you make on your repo, `./gameserver uf` will grab new files. If you make a change and that `./gameserver uf` don't get them, it means you were too quick, and that your curl still have old files in cache; in this case, you'll need to wait a few minutes to get your modifications.

## How to test

You need to make sure that all needed commands displayed in opt work properly.
So just run `./gameserver` to show available commands, then try commands one by one.
Common procedure is to first work on command_install, then start, then stop, then debug, then details, then monitor.

## Oops, i found a bug !

If your found a bug, either you'll instantly know how to fix it, or you won't. And either it will be a bug caused by your own code or a bug into LGSM itself. So let's address those cases.

1. It's caused by your own code parts and you know how to fix it: Just go on and fix it.
2. It's caused by your own code parts but you got no idea why: Use `./gameserver dev-debug` that will add a very detailed log into your rootdir that might help you figuring this out. To disable the dev-debug mode, just re-run the command. If you still can't find why it's not working, come get help on Discord's #gsm-development channel or Github issue that might have been created for this issue.
3. You found a bug into LGSM itself. First, you need to be sure that it's really a bug that affects every game, by testing with another game onto the original repo, otherwise, if it only affects your game, you will usually just need to add a clever conditional check to fix the issue.