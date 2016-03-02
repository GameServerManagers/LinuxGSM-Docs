The stop function will attempt to gracefully shutdown the server if possible then use tmux to end a session

All Source engine servers support graceful shutdown by sending a command via "tmux send" command