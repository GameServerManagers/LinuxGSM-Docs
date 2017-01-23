LinuxGSM provides a few commands to help developers.

## dev-debug

- Generates a lockfile activating the mode
- Generates a full log of commands and tests that the whole script does which might help you debugging your work while coding.

````bash
./gameserver dev-debug
./gameserver dev
````

## deps-detect

Detects dependencies the server binary requires using serverfiles content.

````bash
./gameserver detect-deps
./gameserver dd
````

## detect-glibc

Automatically detects the version of GLIBC that is required.

````bash
./gameserver detect-glibc
./gameserver dg
````

## detect-ldd

Automatically detects required deps using ldd.

````bash
./gameserver detect-ldd
./gameserver dl
````