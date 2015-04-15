
LGSM uses tmux to run servers in the background so the instance is not lost when you close a terminal session.

Tmux is a key component of LGSM and replaced [screen] which was used on early versions of LGSM. tmux has a few improvements over screen; mainly being better at handling of non root users which was a major issue when developing LGSM with screen. tmux allows LGSM to call up a game server running an the background so you can see what it is doing; this feature is available with console feature of LGSM.

LGSM requires _tmux =\> 1.6_ to enable console logging.

Known Issues
------------

tmux 1.8 has an issue that prevents console logging from working. This is because the `pipe-pane` feature is broken in tmux 1.8 causing is not to output the console to the console log files. The only solution is to use another version of tmux.

<http://sourceforge.net/p/tmux/mailman/message/32033641/>

![Tmux Terminal](https://github.com/dgibbs64/linuxgsm/blob/master/images/screens/Tmux.png)

External links
--------------

[tmux Homepage][]

  [LGSM Console using tmux]: Tmux.PNG‎ "fig:LGSM Console using tmux"
  [screen]: http://en.wikipedia.org/wiki/GNU_Screen
  [tmux Homepage]: http://tmux.sourceforge.net/