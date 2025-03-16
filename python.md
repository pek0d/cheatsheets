# Python hints

## Работа с пакетами

показать устаревшие пакеты  
`pip list --outdated`  
обновить пакет  
`pip install -U <package name>`  
пакет который обновляет все устаревшие пакеты  
`pip install pip-review`  
обновление в интерактивном режиме  
`pip-review --local --interactive`  
обновление в автоматическом режиме  
`pip-review --local --auto`  
удалить пакеты  
`pip freeze > to_remove.txt`
`pip3 uninstall -y -r <(pip3 freeze)`  
`pip uninstall -y -r <(pip freeze)`

## Создание виртуального окружения

создание
`python3 -m venv venv`  
активация окружения
`source venv/bin/activate`  
[Подробности](https://docs.python.org/3/library/venv.html)
деактивация окружения
`deactivate`

## Установка модулей

установка модуля (пакета) который импортируется в коде  
`python3 -m pip install <package name>`  
или `pip install <package name>` или `pip install -r requirements.txt`

## Запуск скрипта без добавления в PATH

Внутри самого файла со скриптом прописать "Шебанк"
**#!/usr/bin/env python3**

`chmod +x <file>`  
`sudo ln -s $(pwd)/<file> /usr/local/bin`

