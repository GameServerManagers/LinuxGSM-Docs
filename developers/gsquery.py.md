# monitor\_gsquery.py

## What is gsquery ?

gsquery is a python module to LinuxGSM that can query a game server port to see if it responds.

It is used by the \[\[Monitor\]\] function to make sure that your server is online and responding to queries.

## How to use

Simply use the \[\[Monitor\]\] function, and if gsquery is present, it will be used.

## Manual usage

gsquery can also be used manually. There is a help option for complete list of supported engines/query types.

```text
./gsquery.py -a 1.2.3.4 -p 27015 -e source
```

### Known issue

The only known limit noted to this function has been seen in Garry's Mod, where the server would sometimes be frozen, but still answer to queries.

