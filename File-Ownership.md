# Introduction

Linux files and folders always belong to a user and group. That is what we call ownership.  
Here are some commands to change them.


# Group ownership
Change group ownership on files or folders

### Command
`chgrp`

### Syntax
`chgrp -Args group /path/to/folder/or/file`

#### Recursive
`chgrp -R group /path/to/folder/`


# User and group ownership
Change user and/or ownership for files and folders

### Command
`chown`

### Syntax
`chown -Args user /path/to/folder/or/file`  
`chown -Args user:group /path/to/folder/or/file`

#### Recursive
`chown -R`