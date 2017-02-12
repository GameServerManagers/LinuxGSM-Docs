# Introduction

Linux files and directories always belong to a user and group. That is what we call ownership.  
If this can be boring to new users, remember that this is a huge part of what makes Linux as secured as it is.  

# Check current ownership
## Check ownership in the current directory:
`ls -l`  

Example output:

```
ultimatebyte@game:~$ ls -l
total 32
drwxr-xr-x 5 ultimatebyte ultimatebyte 4096 Jan 29 22:26 lgsm
drwxr-xr-x 5 ultimatebyte ultimatebyte 4096 Jan 29 22:23 log
drwxr-xr-x 4 ultimatebyte ultimatebyte 4096 Jan 29 22:26 serverfiles
drwxr-xr-x 8 ultimatebyte ultimatebyte 4096 Jan 29 22:26 Steam
drwxr-xr-x 5 ultimatebyte ultimatebyte 4096 Jan 29 22:24 steamcmd
-rwxr-x--- 1 ultimatebyte ultimatebyte 5691 Jan 30 01:14 twserver
```

Syntax of the output is:  
* `d` for directory or `-` for file
* user, then group, then others permissions
* number specifies the number of links or directories inside of a directory
* The user that owns the file, or directory
* The group that file or directory belongs to
* The size in bytes
* The date of last modification
* The name of the file

## Check ownership from all files and hidden files of any directory

`ls -al /path/to/file/or/dir`

Sample output:

```
ultimatebyte@game:~$ ls -al /home/ultimatebyte
total 132
drwxr-xr-x 11 ultimatebyte ultimatebyte  4096 Feb  2 07:36 . # Ownership from the current given dir
drwxr-xr-x 22 root         root          4096 Feb  2 07:36 .. # Ownership from the parent dir
-rw-------  1 ultimatebyte ultimatebyte 49744 Feb 12 03:04 .bash_history
-rw-r--r--  1 ultimatebyte ultimatebyte   220 Apr 15  2016 .bash_logout
-rw-r--r--  1 ultimatebyte ultimatebyte  3515 Apr 15  2016 .bashrc
drwxr-xr-x  4 ultimatebyte ultimatebyte  4096 Jan 15 23:26 .config
drwxr-xr-x  5 ultimatebyte ultimatebyte  4096 Jan 29 22:26 lgsm
drwxr-xr-x  3 ultimatebyte ultimatebyte  4096 Jan 14 18:10 .local
drwxr-xr-x  5 ultimatebyte ultimatebyte  4096 Jan 29 22:23 log
-rw-------  1 ultimatebyte ultimatebyte  1005 Jan 30 01:14 .nano_history
-rw-r--r--  1 ultimatebyte ultimatebyte   675 Apr 15  2016 .profile
-rw-r--r--  1 ultimatebyte ultimatebyte    66 Sep  1 17:43 .selected_editor
drwxr-xr-x  4 ultimatebyte ultimatebyte  4096 Jan 29 22:26 serverfiles
drwxr-xr-x  3 ultimatebyte ultimatebyte  4096 Jan 15 01:40 .steam
drwxr-xr-x  8 ultimatebyte ultimatebyte  4096 Jan 29 22:26 Steam
drwxr-xr-x  5 ultimatebyte ultimatebyte  4096 Jan 29 22:24 steamcmd
-rwxr-x---  1 ultimatebyte ultimatebyte  5691 Jan 30 01:14 twserver
-rw-r--r--  1 ultimatebyte ultimatebyte    29 Jan 30 02:17 .tw-server.lock
```

# All these commands require elevated privileges!

# Change owner
Change owner from files or directories

## Command 
`chown`

As usual, `chown --help` will provide you with all available arguments

### Single file syntax
`chown newowner /path/to/file/or/directory`

### Recursive syntax (include sub files and directories)
`chown -R newowner /path/to/directory`

### Example

`chown -R myuser /home/myuser`


# Group ownership
Change group ownership on files or directories

## Command
`chgrp`

As usual, `chgrp --help` will provide you with all available arguments

## Single file syntax 
`chgrp newgroup /path/to/dir/or/file`  


## Recursive syntax (include sub files and directories)
`chgrp -R newgroup /path/to/dir/`


# User and group ownership
Change user and/or ownership for files and directories at the same time

## Command
`chown`

As usual, `chown --help` will provide you with all available arguments

## Single file command
`chown user:group /path/to/dir/or/file`

## Recursive
`chown -R user:group /path/to/dir`

### Example:

chown -R myuser:myuser /home/myuser

