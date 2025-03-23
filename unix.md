# UNIX-hints

`uname` view system info (linux)  
`uname -srm`
`uname -n`
`uname -v`
`uname -r` - view about kernel release info
`uname -m` - view machine hardware info
`uname -a` - view all info
`sudo lshw`- view hardware info
`sudo lshw`- short view hardware info short
`sudo lshw -html > lshw.htmlw` - save info in html file
`lscpu view` - view info cpu
`sudo lsblk` - view block devices (all drives)
`sudo lsusb` - view usb info
`cat /proc/cpuinfo | grep "model name" | uniq` - check CPU architecture
`uname -m`
`curl -L "URL"` - download file from URL
`curl -L https://gist.github.com/lilydjwg/fdeaf79e921c2f413f44b6f613f6ad53/raw/94d8b2be62657e96488038b0e547e3009ed87d40/colors.py | python3` -

## time fix for dualboot (win-linux)

`sudo timedatectl set-local-rtc 1 --adjust-system-clock`
проверка времени `timedatectl`
проверка служб `sudo systemctl list-units --state=running`
switching linux kernels  
`sudo mhwd-kernel --listinstalled`  
`sudo mhwd-kernel --list`  
`sudo mhwd-kernel --install linux61`

## SSH

`ssh -p '2255' pekod@192.168.88.242` - connect to server with port 2255  
Сгенерировать ssh ключи (можно без passphrase)  
`ssh-keygen -t rsa -b 4096`  
Добавить пароль сервера в ssh (чтобы не вводить при каждом подключении).Для этого нужно хотя бы раз войти на сервер.
`ssh-copy-id user@server`  
Дополнительно (если все таки просит пароль) нужно проставить права на сервере (куда скопирован ключ)
`chmod go-w /home/user`
`chmod 700 /home/user/.ssh`
`chmod 600 /home/user/.ssh/authorized_keys`
`sudo systemctl restart sshd.service`

## mikrotik

`/tool wol mac=FE:4B:71:05:EA:8B` пробудить хост по мак адресу

## rsync

copy notes dir to NAS with check before execute
`rsync -rv --dry-run -e "ssh -p 2255" notes pekod@192.168.88.242::NetBackup or rsync -chavzP --rsh="ssh -p 2255" <source> pekod@192.168.88.242::NetBackup/notes`
copy file from NAS (add rsync user on NAS before)
`rsync -chavzP --stats -e 'ssh -p 2255' pekod@192.168.88.242::NetBackup/file(dir) ~/`
rsync with delete files at target folder
`rsync -chavzP -r --delete -e "ssh -p 2255" .config/alacritty/alacritty.yml pekod@192.168.88.242::NetBackup`

## GPG & pass

`gpg --import public.gpg secret.gpg`
GPG trust key activate
`gpg --edit-key "onathema@gmail.com"`
trust key 5
gpg encrypt file `gpg -e -a -r onathema@gmail.com file.csv`
gpg decrypt file `gpg -d -o file.csv file.csv.asc`
check keys `gpg -K`

## Docker

`docker info` - show info about current docker engine version
`docker ps -a` - show all containers
`docker ps -q` - show only container ID
`docker system df` - show disk usage
`docker system df -v` - show disk usage by volumes
`docker volume ls` - show all volumes
`docker volume ls -q` - show only volume ID
`docker volume rm [volume ID]` - remove volume
`docker container rm [container ID]` - remove container
`docker container stop [container ID]` - stop container
`docker container start [container ID]` - start container
`docker container restart [container ID]` - restart container
`docker container logs [container ID]` - show logs container
`docker stop $(docker ps -a -q)` - stop all containers
`docker rm $(docker ps -a -q)` - remove all containers
`docker rmi $(docker images -q)` - remove all images
`docker-compose up -d` - start docker-compose
`docker build -t [BOT NAME] .` создание отображаемого docker-образа
`docker run --env-file .env --name bill_bot -d bill_bot` запуск бот с env-файлом (с переменным окружением)
**Важно чтобы в файле .env был явно укзана токен BOT_TOKEN=**

**контейнеры можно обновлять с помощью контейнера WATCHTOWER**

`docker-compose logs -f` - follow logs
`docker build command` - build docker image

## macOS

Tune auto-hide dock
`defaults write com.apple.dock autohide-time-modifier -float 0.15; killall Dock`
Reset login items and background tasks in preferences menu  
`sfltool dumpbtm`

## Git

git add remote server with other ssh port  
`git remote add origin ssh://pekod@192.168.88.242:2255/volume1/gitsyno/repo.git`
git clone from server to local  
`git clone ssh://pekod@192.168.88.242:2255/volume1/gitsyno/repo.git`
Create git repo on server  
`mkdir /git/[category]/test.git`  
`cd /git/[category]/test.git && git init --bare --shared`  
push files from local to remote server  
`git push [category] [branch name]`
`git push -u origin master`
create and initialize an empty repository  
`git init`
add a remote named origin for the repository at repository  
`git remote add origin <repository>`
check out the master branch  
`git checkout master`
Update git repo  
`git pull`
watch git changes  
`git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit`
спрятать изменения git  
`git stash`
показать изменения git  
`git stash pop`
If git branch develop, fatal: Not a valid object name: 'master'  
`git config --global user.name "Thinker.What"`
`git config --global user.email "onathema@gmail.com"`
`touch README`
`git add README`
`git commit -m 'init README'`
Create Zip file from repo  
`git archive [branch name] | bzip2 > ~/Desktop/[project name].zip`
А вот отменить изменения сделанные в последнем коммите можно с помощью команды `git revert`
Она делает еще один коммит, но с противоположными изменениями.
`git pull strategy`
`git pull --no-ff origin main`

## CLI utilities & commands

`grep "word" -r /path/` - поиск по слову в каталоге
проверка режима терминала `infocmp` or `toe`  
`echo=$TERM`
Для работ клавиш стрелок, удалить нужно сменить переменную TERM
`TERM=xterm-256color`
port check `netstat -vanp tcp | grep 5`
cd into directory without having permission `sudo su cd directory`
diskusage human language (сколько места занято на диске) `du -shx` or `df -hl`
check dns `scutil --dns | grep 'nameserver\[[0-9]*\]'`
скрыть/показать файл(Shift+command+.)
`chflags hidden file/folder defaults write c`
`chflags nohidden file/folder`
moves us back two levels. `cd ../..`
show all files including hidden `ls -a`
show current directory (Print Working Directory) `pwd`
показать содержимое файла `bat` or `cat файл`
показывает место измнений в файле `bat -d`
print history of commands in terminal `history`  
`history -d [linenumber]`
clear history (purge) `history -p`  
`history -c`
display a line of text `echo`
посмотреть количество файлов и каталогов `tree`
moving mouse on default mac os terminal (alt+left click)
посмотреть статистику файла-каталога `stat -x file/directory`
посмотреть какие файлы изменились за последние 24 часа `find . -type f -mtime 0`
посмотреть какие файлы изменились за последние 24 часа и вывести их в список `find . -type f -mtime 0 -print0 | xargs -0 ls -l`
посмотреть какие файлы изменились за последние 24 часа и вывести их в список `find . -mtime 0 -exec ls -l {} \;`
посмотреть какие файлы изменились за последние 24 часа и вывести их в список `find . -mtime 0 -exec ls -l {} \; | grep -v "total"`
изменение размера шрифта в alacrtitty `alacritty -o font.size=12.25`
suspend process (ctrl+z)
return to process `fg`
kill process (ctrl+c) или q
утилита сравнения файлов по строкам `diff file1 file2`
снятие карантина с приложухи в macOS `xattr -dr com.apple.quarantine /Applications/Chromium.app`
смена прав на полные (чтоб хайлайт файла был красным) `chmod 755 file`
проверка работы курсива в терминале
`echo -e "\e[3mfoo\e[23m"`
`echo -e "\e[1mbold\e[0m\n\e[3mitalic\e[0m\n\e[4munderline\e[0m\n\e[9mstrikethrough\e[0m"`
принудительная очистка корзины `sudo rm -r ./.Trash/\*`
переключение питона на версию 3.11
`pyenv install 3.11` or `pyenv global 3.11`
`echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc`
`echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc`
`exec zsh`
`source ~/.zshrc`
Unarchive tar archive `tar -xvf`
Install oh-my-zsh `sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`
zsh-autosuggestions `git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions`
zsh-fast-syntax-highlighting plugin `git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting`
zsh-autocomplete plugin `git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git $ZSH_CUSTOM/plugins/zsh-autocomplete`

## Fzf

keybings To install useful keybindings and fuzzy completion(apple silicon):  
`$HOMEBREW_PREFIX/opt/fzf/install`  
To install useful key bindings and fuzzy completion: `(brew --prefix)/opt/fzf/install Ctrl+r (Ctrl+t)`  
To install useful key bindings and fuzzy completion for tmux: `(brew --prefix)/opt/fzf/install --tmux`  
To install useful key bindings and fuzzy completion for zsh: `(brew --prefix)/opt/fzf/install --zsh`

## SAMBA

`mount smb` - create mounting point
`mkdir sd`
`mount_smbfs //pekod@nas.local/home/Drive ./sd`
`umount ./sd`
`sudo mount_smbfs //pekod@nas.local/home/Drive ./sd`
`touch /etc/samba/smb.conf` - create config file
`sudo nano /etc/samba/smb.conf` - edit config file
`sudo smbpasswd -a pekod` - add user
Print server on arch linux `yay -Sy --noconfirm cups`
`/etc/cups/cupsd.conf` edit cupsd.conf  
`cupsctl --remote-admin --remote-any --share-printers` - allow remote access to all connected printers
Print server on macOS `brew install cups`
[что такое CUPS](https://help.ubuntu.ru/wiki/%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_ubuntu_server/%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B5_%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0/cups)

## Homebrew

`brew bundle dump` create brewfile
`brew bundle install --file /path/tobrewfile` установка всех необходимых пакетов
`brew bundle check` проверка наличия всех необходимых пакетов
`eza --icons -la -s=type` показывает список файлов и папок с иконками

## ffmpeg cases

`ffmpeg -i input -c:v copy -c:a aac output`
`ffmpeg -i input -vcodec copy -acodec copy -c:s mov_text -map 0 -tag:v hvc1 output.mp4`
`ffmpeg -i input.mp3 -c:a aac -vn output.m4a`
`ffmpeg -i input -vn -acodec copy output.m4a`
`ffmpeg -i input -c:v libx265 -crf 28 -c:a aac -b:a 128k output.mp4`
`ffmpeg -i input.mkv -vn -c:a libfdk_aac -b:a 256k output.m4a`
Merging video and audio, with audio re-encoding `ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac output.mp4`

## yt-dlp

Параметры загрузки
`mkdir -p ~/.config/youtube-dl/`
`echo "-o ~/Downloads/%(title)s.%(ext)s" > ~/.config/youtube-dl/config`
загрузка различных вариантов
`yt-dlp -f bestaudio --extract-audio --audio-format m4a --audio-quality 0 <Video-URL>`
`yt-dlp -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best' <Video-URL>`
convert to hevc
`yt-dlp "URL" --postprocessor-args "-c:v libx265 -preset ultrafast -crf 23 -tag:v hvc1 -c:a aac" --merge-output-format mp4`
opus audio
`yt-dlp "URL" --postprocessor-args "-c:v libx265 -preset fast -crf 15 -c:a opus -strict experimental -b:a 128k" --merge-output-format mp4`
403 forbidden
`yt-dlp -f 299+251` --no-cache-dir URL
`yt-dlp --rm-cache-dir`
list of formatsn `yt-dlp <URL> -F`
download in needed format `yt-dlp -f (number_audio+number_video) <URL>`
video format
`--format bestvideo[ext=mp4]+bestaudio[ext=m4a]/bestvideo+bestaudio`
`--merge-output-format mp4`

## imagemagick

Add border (sample) `convert testing.png -border 1x1 -bordercolor black result.png`
Resize (sample) `convert testing.png -resize 1920 (or x1080) example.png`
Add effect (sample) `convert testing.png -charcoal 2 example.png`
Batch resize (sample)
`for file in *.png; do convert $file -resize 1920 small-$file; done`
Batch convert `mogrify -format heic *.jpg`
`convert heic *.jpg`

## exiftool

`exiftool '-filemodifydate<datetimeoriginal>' <file>`

## ZFS

`sudo zfs set mountpoint=/mnt/zfspool zfspool` монтирование пула
`sudo zpool set autoexpand=on zfspool` автоматическое расширение пула
добавить в _/etc/udev/rules.d/90-zfs.rules_ `KERNEL=="sd*", ACTION=="add", RUN+="/usr/bin/zpool import zfspool"` dev-правила для автоматического импорта
`sudo udevadm control --reload-rules` обновление udev
`zpool status datapool` покажет состояние пула
`zfs list` список дисков с zfs
`df -h /mnt/mydata` покажет занятое пространство
