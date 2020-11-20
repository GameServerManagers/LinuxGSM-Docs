# mods

LinuxGSM supports the installation, updating, and removing of selected mods and add-ons for some games and engines.  
Zip add-ons are currently the only supported installations.

## Commands

### Install mods

`./gameserver mods-install`

`./gameserver mi`

### Update mods

`./gameserver mods-update`

`./gameserver mu`

### Remove mods

`./gameserver mods-remove`

`./gameserver mr`

## Supported mods/add-ons

\(This list was last updated on 2020-11-19\)

### Goldsrc Engine Games (v20.6.0+)
* Metamod
* AMX Mod X

###### Additional Game Specific **AMX Mod X** addons:
* Counter-Strike 1.6
* Day of Defeat
* Team Fortress Classic
* The Specialists
* Natural Selection

### Source Engine Games

* Metamod: Source
* SourceMod

#### For Garry's Mod

* ACF
* ACF Missiles
* DarkRP
* DarkRP Modification
* PAC3
* UClip
* ULib
* ULX
* UTime

### Unity3D Games

Rust, Hurtworld, 7 Days To Die

* Oxide Mod

## Technical Details

### Install

* All available mods are defined in the mods\_list.sh.  
* Mods hosted on github use the latest archive link available. Others are scraped through a mods download mirrors in order to find the latest version.  
* If some mods are already installed, a list of installed mods shows up. If a user tries to install a mod that is already installed, there will be a warning that any custom files will be overwritten.  
* A list of available mods is displayed to the user, including the developers website.  
* After the user selects a mod, the file gets downloaded and extracted to a temporary directory.  
* A list of the mod files is created at `lgsm/mods/modname-files.txt`. This list allows the mod to be removed if required. LinuxGSM developers have whitelisted important customisable files such as mod config files that will not be removed. If there are any important files that have been missed please raise an issue.
* Files and directories then get copied to the correct destination.
* LinuxGSM updates a file containing a list of installed mods `lgsm/mods/installed-mods.txt`.

### Update

* The list `lgsm/mods/installed-mods.txt` is used to identify which mods are installed. If a non-referenced mod is found, the updater will stop with an error.
* Three update types are available
  * OVERWRITE will overwrite all mod files.
  * NOUPDATE will prevent this mod from being updated. Useful for a framework that is designed to be entirely customized.
  * RETAIN keeps the whitelisted files and updating everything else.
* As there is no easy way to check for mod versions, the update process will update every single installed mod every time the command is run.
* The process is pretty similar as the installation, mod gets downloaded, extracted, files get removed. Removed files go to a temp file list, then file list list built and temp file list added to it. Finaly the mod gets copied to destination using `cp -Rf`.
* If an admin wants to overwrite custom files, then he can either uninstall/reinstall the mod, or just install over it.

### Remove

* A list of installed mods is displayed, user has to pick one to remove.
* Any file listed in `lgsm/mods/modname-files.txt` gets removed.
* The file list gets removed, as well as the entry in `installed-mods.txt`.

## Adding mod support

### What mods can be added

Any as long as the archive can be found online and the installation consists of extracting an archive to the `serverfiles` directory.

### Asking to add support for a mod

If there is a mod you wish to see supported by LinuxGSM please raise a GitHub issue with any relevant info about the mod.

### Developers

If you wish to create a pull-request yourself for this, please make sure you read the "Developer" section at the bottom right of the wiki.

Usually, editing mods\_list.sh should be enough to add mod support. This script contains comments helping you to understand how to use it.

Basically: Add an array variable containing mod info, then add the array to the global array.

Long explanation: The list is based on arrays, used to define all mod properties. You need to make sure that every value is filled up and in the correct order, that mod commands are unique and that multiple choices values are ended with a semicolon \(;\), otherwise the last value will be ignored.  
You might need to add an entry in `fn_mod_tidy_files_list` from `mods_core.sh` in order to remove lines from mod's file list so that they do not get wrongly removed with the mods-remove command. For further assistance on developing this contact UltimateByte who developed those functions and dgibbs that reworked it should be able to help.

