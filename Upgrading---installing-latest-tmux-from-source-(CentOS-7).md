# Preamble
If you are on an older tmux version on CentOS you can upgrade to the latest version following this guide.

**NOTE:** you will be compiling tmux from source, meaning your package manager will not take care of future upgrades.

**NOTE:** Any extra requirement like git,tar is upto you to install

## Getting the requirements

* tmux has a library dependency on _libevent_ which, of course, is not installed by default. 

1. wget https://github.com/downloads/libevent/libevent/libevent-2.0.21-stable.tar.gz
2. tar -xzvf libevent-2.0.21-stable.tar.gz
3. cd libevent-2.0.21-stable
3. ./configure
4. make
5. sudo make install

## Getting tmux source

* Grabbing the tmux source

1. git clone https://github.com/tmux/tmux.git
2. cd tmux
3. sh autogen.sh
4. ./configure
5. make

## Verify you are on the latest tmux.

1. tmux -V

(currently: tmux 2.3)

## Possible problems

* If you encounter 'libevent not found' during the tmux compiling/install.

1. yum install libevent-devel

* If you encounter 'curses not found' during the tmux compiling/install.

1. yum install ncurses-devel
2. yum install glibc-static