# Python and PIP hints

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

создание окружения  
`python3 -m venv /path/to/new/virtual/environment`  
чаще всего если уже в каталоге проекта  
`python3 -m venv venv`  
активация окружения  
`source venv/bin/activate`  
[Подробности](https://docs.python.org/3/library/venv.html)
деактивация окружения  
`deactivate`

## Установка модулей

установка модуля (пакета) который импортируется в коде  
`python3 -m pip install <package name>`  
или  
`pip install <package name>`

## запуск python скрипта без добавления в PATH

Внутри самого файла со скриптом прописать "Шебанк"
**#!/usr/bin/env python3**

`chmod +x <file>`  
`sudo ln -s $(pwd)/<file> /usr/local/bin`


## install pyenv on Ubuntu 20.04
`sudo apt update && sudo apt -y upgrade`
`python3 -V`
`sudo apt install -y python3-pip`
`pip3 install package_name`
`sudo apt install -y build-essential libssl-dev libffi-dev python3-dev`
`setting python3 environment`
`sudo apt install -y python3-venv`
`mkdir environments`
`cd environments`
`python3 -m venv my_env`
`ls my_env`
`source my_env/bin/activate`