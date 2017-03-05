LinuxGSM now supports installing, updating, and removing some mods and addons for some games and engines.  
We currently support zip addons installations only. Other mods for other games are still to be installed manually.

# Commands

## Install mods
`./gameserver mods-install`

`./gameserver mi`
## Update mods
`./gameserver mods-update`

`./gameserver mu`
## Remove mods
`./gameserver mods-remove`

`./gameserver mr`

# Supported mods/addons

(This list was lastly updated on 2017-01-28)

## For Source Engine Games
* metamod
* sourcemod (1.8)

## For Garry's Mod
* ULib
* ULX
* UTime
* UClip
* ACF
* ACF Missiles
* DarkRP
* DarkRP Modification

## For Unity3D games (Rust/Hurtworld/7 Days To Die)
* Oxide Mod

# How does it work?

### Install
* All available mods are defined into mods_list.sh.  
* For mods hosted on github, the latest archive link is used. For others, we're scraping through mod's mirrors in order to find the latest file.  
* If some mods are already installed, then a list of installed mods shows up. If a user tries to install an already installed mod, he's warned that any custom file will be overwritten.  
* A list of available mods is displayed to the user, including developer website for every single one.  
* After the user selects a mod, the file gets downloaded, then extracted.  
* A file containing mod's file list relative to extract dir is created: `lgsm/mods/modname-files.txt`. Those file lists are used in order to allow uninstalling a mod properly, while making our best to keep sensitive directories safe by removing them from the list, using `fn_mod_tidy_files_list` from `mods_core.sh`.
* Then files and directories get copied to the destination using `cp -Rf`.
* LinuxGSM then creates a file containing a list of installed mods: `lgsm/mods/installed-mods.txt`, allowing to know: how many mods are installed; is the mod we're trying to install already installed; and what mods to update. 

### Update
* The list `lgsm/mods/installed-mods.txt` is used to know what mods are installed. If a non-referenced mod is found, the updater will stop with an error.
* Three update mods are available: OVERWRITE will like the name says, overwrite every mod's files; NOUPDATE will prevent this mod from being updated if it's for example a framework that is designed to be entirely customized; the last mode is a list of paths, relative to the mod's extract dir, that will be removed after extraction in order to not overwrite user ones, which is pretty useful to make sure we're not overwriting any config or usually customized file.
* As there is no easy way to check for mod's version, the update process will update every single installed mod every time the command is run.  
* Then the process is pretty similar as the installation, mod gets downloaded, extracted, files get removed, and removed files go to a temp file list, then file list list built, and temp file list added to it, then the mod gets copied to destination using `cp -Rf`.
* If a user wants to overwrite custom files, then he can either uninstall/reinstall the mod, or just install over it.

### Remove
* A list of installed mods is displayed, user has to pick one to remove. If none, it exits.
* Any file listed in `lgsm/mods/modname-files.txt` gets removed with `rm -Rf`.
* This file list gets removed, as well as the entry in `installed-mods.txt`

# Adding mod support

## What mods can be added
As long as the archive can be found over the net and that the installation consists in extracting the file somewhere in serverfiles directory, then adding support for the mod should be quite easy. 

## Asking to add support for a mod
If there is a mod you wish to see supported by LinuxGSM, please, contact us on Discord or open a Pull-Request on Github with relevant information.

## Developers

**Reminder**: If you wish to pull-request yourself for this, please make sure you read the "Developer" section at the bottom right of the wiki.

Usually, editing mods_list.sh will be enough to add mod's support. This script contains comments helping you to understand how to use it.  

Basically: Add an array variable containing mod info, then add the array to the global array.

Long explanation: The list is based on arrays, used to define all mod properties. You just need to make sure that every value is filled up and in the correct order, that mod commands are unique, and that multiple choices values are ended with a semicolon (;), otherwise the last value will be ignored.  
You might need to add an entry in `fn_mod_tidy_files_list` from `mods_core.sh` in order to remove lines from mod's file list so that they don't get wrongly removed upon mods-remove command. For further assistance on developing this, UltimateByte that introduced those functions and dgibbs that deeply reworked it might be able to help.