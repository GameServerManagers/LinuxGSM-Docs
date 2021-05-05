# Symlinking and ln command

Symlinks create multiple paths to a file or directory and are useful for saving space or having 1 set of files for multiple installs.

## Using Symlinks to Save Storage Space

This guide is for pointing multiple directories to the same folder using `ln` command. Ln creates hardlinks and softlinks, the -s variable creates softlinks. These can be compared to shortcuts on windows, and are going to be used in this guide.

Example guide using two "one server + one user" installs with Sven Co-op:

`Gameserver folder 1: /home/svencoop/serverfiles/svencoop_downloads/`

`Gameserver folder 2: /home/svencoop2/serverfiles/svencoop_downloads/`

`Shared folder /home/svencoop_content/svencoop_downloads/`

The command to link these would be `ln -s /shared_folder/ /gameserver_folder/`

`ln -s /home/svencoop_maps/svencoop_downloads/ /home/svencoop/serverfiles/`

`ln -s /home/svencoop_maps/svencoop_downloads/ /home/svencoop2/serverfiles/`

Change the game server folder ownership to be under their respective users and you are done.

`chown svencoop /home/svencoop/serverfiles/svencoop_downloads`

`chown svencoop2 /home/svencoop2/serverfiles/svencoop_downloads`

The files in the symlinks do not need be owned by the gameserver users and will not be recognized by linuxGSM's ownership check. That being said, make sure they can be read by the gameserver users. 

## Symlink resources

[Excellent description of differences between Symlinks and Hardlinks by OSTechNix](https://www.ostechnix.com/explaining-soft-link-and-hard-link-in-linux-with-examples/)

[Official Ubuntu ln Documentation](http://manpages.ubuntu.com/manpages/disco/man1/ln.1.html)

