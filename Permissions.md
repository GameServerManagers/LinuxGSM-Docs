## Introduction
In Linux, files are owned by a user and a group. On top of that, this user, group, and other ones (groups and users), have different permissions on these files. That's what we call file permissions.  
You might need to change them. Here are some useful commands.

# Permissions
Change permissions for user, groups, and others on files and folders.

## Permissions Command 
`chmod `

### Permissions Syntax 
`chmod -target+/-permissions /path/to/folder/or/file`

#### Permissions recursive argument syntax
`chmod -R -target+/-permissions /path/to/folder/`

### Permissions add
`chmod +rwx filename`  
Will add read, write, and execute permissions to this file anyone on the machine.
r stands for "read", w for "write", and x for "execute"

Example : `chmod +x filename`  
Will make the file executable by anyone on the machine.

### Permissions remove
`chmod -rwx filename`
Will remove read, write, and execute permissions to this file anyone on the machine.  
Note : root user is the only exception.

### Permissions for user/group/others/all
`chmod -u+rwx`  
`chmod -g+rwx`  
`chmod -o+rwx`  
`chmod -a+rwx`  

### Multiple permissions at once
`chmod -u+r,g-w,o-rwx`  

### Copy permissions from a group to another
`chmod dest=source`  

Example : `chmod -R g=u /home/userdir/subfolder`  
Will recursively give the owner group the same rights as the user group.

## Set all permissions at once

`chmod 777` == `chmod -a+rwx`  
`chmod 000` == `chmod -a-rwx`  

First number is for user, second is for group, third for others

### Values

````
0 no permissions
1 x
2 w
3 wx
4 r
5 rx
6 rw
7 rwx
````

### Set GUID
No GUID

`chmod -R a-s /path/to/folder`  
`chmod -R 0xxx /path/to/folder `

Example : `chmod -R 0640 /home/user/website`  

#### Set UID
Files will run as the user

`chmod -R u+s /path/to/folder/`  
`chmod -R 2xxx /path/to/folder`

#### Set GID
Any subfolder and subfile will have the same group

`chmod -R g+s /path/to/folder/`  
`chmod -R 4xxx /path/to/folder`

#### Set GUID
Set both UID and GID

`chmod -R a+s /path/to/folder/`  
`chmod -R 6xxx /path/to/folder`