# console

The `console` command allows access the output of the game server executable. Depending upon which server you are running it can allow you to see the current activity of the game server, check errors in real time, and input commands.

> Note: Different game servers provide different features in console, so results will vary. For example some allow user input and others do not. While some give a very verbose output and others next to nothing \(looking at you rust!\).

## Commands

Run the following command to access console:

Standard: `./gameserver console`

Short: `./gameserver c`

Answer **y** at the prompt.

## Exiting the console

To exit the console: Press **CTRL + b**, then, press **d**

> Take your time with this as it can be confusing at first.

### Do not exit the console using CTRL+c

Pressing `CTRL+c` while in console will instantly kill the tmux session, stopping the game server.

