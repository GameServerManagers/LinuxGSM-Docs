# Stop Mode

Stop mode allows a game server to gracefully shutdown by sending a stop signal to the server. The stop signal might be one of the various commands such as `stop`,`quit`,`exit` etc. In some cases, this is important to give the server time to save its state.

```text
# Stop Mode | https://docs.linuxgsm.com/features/stopmode
# 1: tmux kill
# 2: CTRL+c
# 3: quit
# 4: quit 120s
# 5: stop
# 6: q
# 7: exit
# 8: 7 Days to Die
# 9: GoldSrc
# 10: Teamspeak 3
stopmode="7"
```



