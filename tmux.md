## TMUX hint

Создание окна тмукса если такого ещё нет — создаёте новый  
`tmux attach || tmux new`  
перезапуск тмукса  
`tmux kill-server && tmux`  
config reload (apply changes)  
`tmux source ~/.tmux.conf`  
change config path (tmux config file "tmux.conf")  
`tmux -f path-to-config`  
**Файл конифга должен быть видимым!**

swap windows in tmux order (add to .tmux.conf)  
`bind-key T swap-window -t 0`  
включение set -g  
`tmux show -g | sed 's/^/set -g /' > path-to-config-tmux.conf`  
prefix  
`Ctrl+b`  
отключиться  
`Ctrl+b d`  
создать окошко;  
`Ctrl+b c`  
перейти в такое-то окошко  
`Ctrl+b 0...9`  
перейти в предыдущее окошко  
`Ctrl+b p`  
перейти в следующее окошко  
`Ctrl+b n`  
перейти в предыдущее активное окошко (из которого вы переключились в текущее)  
`Ctrl+b l`  
закрыть окошко (а можно просто набрать exit в терминале)  
`Ctrl+b &`  
разделить текущую панель по вертикали  
`Ctrl+b %`  
разделить текущую панель по горизонтали (это кавычка, которая около Enter)  
`Ctrl+b "`  
переход между панелями  
`Ctrl+b →← ↑↓`  
закрыть панель (а можно просто набрать exit в терминале)  
`Ctrl+b x —`  
Fullscreen pane toggle  
`Ctrl+b z`  
Resize panes  
`Ctrl+b Ctrl →← ↑↓`  
вход в «режим копирования», после чего:  
`Ctrl+b PgUp`  
скроллинг  
`PgUp, PgDown`  
выход из «режима копирования»  
`q`  
включение часов  
`Ctrl+b t`  
Переименование окна  
`Ctrl+b ,`  
Open windows tree  
`tmux list-windows`  
`Ctrl+b w`  
install tmux plugins (tmux plugin)  
`Ctrl+b I`  
Менеджер сессий tmux  
`tmuxinator start session-name`

# Installing tmux-256color for macOS

* macOS 10.15.5
* tmux 3.1b

macOS has ncurses version 5.7 which does not ship the terminfo description for tmux.  There're two ways that can help you to solve this problem.

## The Fast Blazing Solution

Instead of `tmux-256color`, use `screen-256color` which comes with system.  Place this command into `~/.tmux.conf` or `~/.config/tmux/tmux.conf`(for version 3.1 and later):

```
set-option default-terminal "screen-256color"
```

The `screen-256color` in most cases is enough and more portable solution.  But it does not support any italic font style.

## The Right Way

Unfortunately, The latest (6.2) ncurses version does not work properly.  Make sure to use ncurses which comes with macOS:  

```
$ which tic
/usr/bin/tic
```

If you see another path to terminal info compiler, you must fix the `$PATH` for a shell, or uninstall a local ncurses by using a package manager.

Let's download and unpack the latest nucurses terminal descriptions:

```
$ curl -LO https://invisible-island.net/datafiles/current/terminfo.src.gz && gunzip terminfo.src.gz
```

And compile `tmux-256color` terminal info.  The result is placed into `~/.terminfo`:

```
$ /usr/bin/tic -xe tmux-256color terminfo.src
```

If you want to use `tmux-256color` for all users, use `sudo`.  The result is placed into `/usr/share/terminfo`:

```
$ sudo /usr/bin/tic -xe tmux-256color terminfo.src
```

You may also to compile few more infos, it is up to you: 

```
$ /usr/bin/tic -xe alacritty-direct,tmux-256color terminfo.src
```

If you see something like:

```
"terminfo.src", line 1650, terminal 'pccon+base': enter_bold_mode but no exit_attribute_mode
"terminfo.src", line 1650, terminal 'pccon+base': enter_reverse_mode but no exit_attribute_mode
```

do not worry, all should be fine.  Make sure that you can use the compiled description:

```
$ infocmp -x tmux-256color
```

And finally, set default terminal in tmux configuration file:

```
set-option default-terminal "tmux-256color"
```

## RGB Colors

Also, do not forget to enable RGB colors (24 bit colors, or true colors, as you like).  The `$TERM` outside tmux must support 256 colors.  Also, it must contains `Tc` or `RGB` flag in terminfo description:

```
$ tmux info | grep -e RGB -e Tc
```

If both are missing, then you need to override terminal description in tmux configuration file:

```
set-option -a terminal-overrides ",XXX:RGB"
```

where `XXX` is a terminal outside tmux, like `xterm-256color`.  And finally, `terminal-overrides` suports a pattern matching:

```
set-option -a terminal-overrides ",*256col*:RGB"
```

If you use [Alacritty](https://github.com/jwilm/alacritty) terminal, make sure the `$TERM` outside tmux is `alacritty-direct`.  The `alacritty` terminal description does not have `RGB` flag.  Otherwise, override description:

```
set-option -a terminal-overrides ",alacritty:RGB"
```