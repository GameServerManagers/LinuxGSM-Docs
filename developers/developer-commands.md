# Developer Commands

LinuxGSM provides a few commands to help developers.

## developer

* Generates a lockfile activating developer mode. All developer options will now show in the list of commands.
* Generates a full output log of everything the script does which can help with debugging.

the log is located is called `dev-debug.log`

```bash
./gameserver developer
./gameserver dev
```

## deps-detect

* Detects dependencies the server binary requires using serverfiles content.

```bash
./gameserver detect-deps
./gameserver dd
```

## detect-glibc

* Automatically detects the version of GLIBC that is required.

```bash
./gameserver detect-glibc
./gameserver dg
```

## detect-ldd

* Automatically detects required deps using ldd.

```bash
./gameserver detect-ldd
./gameserver dl
```
# query-raw
* querys both `gamedig` and `gsquery.py`.

```bash
./gameserver query-raw
./gameserver qr
```
# clear-functions
* deletes all functions in `lgsm/functions` and removes default LinxuGSM configs.

```bash
./gameserver clear-fuctions
./gameserver cf
```
