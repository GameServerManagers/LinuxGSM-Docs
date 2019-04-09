# permissions

In Linux, files and directories are owned by a user and a group \(see [File Ownership](file-ownership.md)\). On top of that, this user, group, and other ones \(groups and users\), have different permissions on these files. That's what we call file permissions.  
You might need to change them.  
If this can be boring to new users, remember that this is a huge part of what makes Linux as secured as it is, and you are required to know this if you wish to do anything serious with Linux.

## Check current permissions

### Check permissions from a file or all files of any directory

`ls -al /path/to/file/or/dir`

Sample output:

```text
ultimatebyte@game:~$ ls -al twserver
-rwxr-x--- 1 ultimatebyte ultimatebyte 5691 Jan 30 01:14 twserver
```

Explanation:

* First character is a a `-` for files, or a `d` for directories
* Three next ones are owner permissions: `rwx`
* Three next ones are group permissions: `rwx`
* Three next ones are "others permissions: `rwx` for groups and users that are now owning the file
* First user listed is the owner
* Next entry is the group owning the file

"r" stands for "read", "w" stands for "write", "x" stands for execute.  
If any letter from `rwx` is showed as a `-`, it means that the permission is not granted.

## Change permissions

Change permissions from files or directories

### Command

`chmod`

### Recursive syntax \(include sub files and directories\)

Append `-R` to your chmod

`chmod -R`

### Syntax 1

Set all permissions at once

`chmod 777` == `chmod -a+rwx`  
`chmod 000` == `chmod -a-rwx`

First number is for user, second is for group, third for others

#### Values

```text
0 no permissions
1 x
2 w
3 wx
4 r
5 rx
6 rw
7 rwx
```

#### Example

Default permissions are 755. If you wish to prevent other users from interacting with your files, then 750 can be great.

`chmod -R 750 /home/userdir`

### Syntax 2

We used `rwx` for these, but of course, you should pick the permissions you wish to add or remove.

#### Permissions add

`chmod +rwx filename`  
Will add read, write, and execute permissions to this file anyone on the machine. r stands for "read", w for "write", and x for "execute"

Example : `chmod +x filename`  
Will make the file executable by anyone on the machine.

#### Permissions remove

`chmod -rwx filename` Will remove read, write, and execute permissions to this file anyone on the machine.  
Note : root user is the only exception.

#### Permissions for user/group/others/all

`chmod -u+rwx`  
`chmod -g+rwx`  
`chmod -o+rwx`  
`chmod -a+rwx`

#### Multiple permissions at once

`chmod -u+r,g-w,o-rwx`

Of course, you can replace `+rwx` by anything previously mentioned

## Set GUID and GID

Advanced permissions management, you will likely not need this for game servers.

### No GUID

`chmod -R a-s /path/to/dir`  
`chmod -R 0xxx /path/to/dir`

Example : `chmod -R 0640 /home/user/website`

### **Set UID**

Files will run as the user

`chmod -R u+s /path/to/dir/`  
`chmod -R 2xxx /path/to/dir`

### **Set GID**

Any subdir and subfile will have the same group

`chmod -R g+s /path/to/dir/`  
`chmod -R 4xxx /path/to/dir`

### **Set GUID**

Set both UID and GID

`chmod -R a+s /path/to/dir/`  
`chmod -R 6xxx /path/to/dir`

