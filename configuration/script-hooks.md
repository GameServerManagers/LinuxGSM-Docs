# Script Hooks

You can create scripts that run before, after, or after in case of error for any command.

## Hook Scripts Location

Relative to your installation directory, create a folder:

```
lgsm/hooks
```

## Script Naming

Script hooks are named according to this convention:

```
hook-<when>-<command>.sh
```

`<when>` can have the values `pre`, `post`, or `error`. Post and error hooks are mutually exclusive and never run within the same command.

`<command>` must match long command names. You can find the commands [here](../commands/README.md). The middle column has the command names. Not the leftmost column with the humand-readable command description.

### Behavior

LGSM will run the script and then continue without checking exit value.

## Notes

Don't forget to make the scripts executable!
