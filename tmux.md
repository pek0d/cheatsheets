# TMUX hint

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

