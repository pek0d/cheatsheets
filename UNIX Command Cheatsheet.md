# UNIX Command Cheatsheet

## System Information

- **View system info (Linux):**
  - `uname` — Display basic system information
  - `uname -srm` — Show kernel name, release, and machine hardware
  - `uname -n` — Display hostname
  - `uname -v` — Show kernel version
  - `uname -r` — View kernel release info
  - `uname -m` — View machine hardware info
  - `uname -a` — Display all system info
- **Hardware info:**
  - `sudo lshw` — View detailed hardware information
  - `sudo lshw -html > lshw.html` — Save hardware info to HTML file
- **CPU info:**
  - `lscpu` — Display CPU details
  - `cat /proc/cpuinfo | grep "model name" | uniq` — Check CPU architecture
- **Storage and devices:**
  - `sudo lsblk` — List block devices (drives)
  - `sudo lsusb` — List USB devices
- **Download files:**
  - `curl -L "URL"` — Download file from URL
  - `curl -L <script_url> | python3` — Execute script from URL (e.g., `https://gist.github.com/.../colors.py`)

---

## SSH

- **Generate SSH key:**
  - `ssh-keygen -t rsa -b 4096` — Create 4096-bit RSA key
- **Copy SSH key to server:**
  - `ssh-copy-id user@server` — Add key to server for passwordless login
- **Set permissions on server:**
  - `chmod go-w /home/user` — Restrict home directory permissions
  - `chmod 700 /home/user/.ssh` — Secure .ssh directory
  - `chmod 600 /home/user/.ssh/authorized_keys` — Secure authorized_keys file
- **open url in host machine via SSH**
  - `ssh -L 9898:127.0.0.1:9898 root@192.168.1.22`

---

## Mikrotik

- **Wake-on-LAN:**
  - `/tool wol mac=FE:4B:71:05:EA:8B` — Wake host by MAC address

---

## Rsync

- **Copy directory to NAS (dry run):**
  - `rsync -rv --dry-run -e "ssh -p 2255" notes pekod@192.168.88.242::NetBackup`
- **Copy with verification:**
  - `rsync -chavzP --rsh="ssh -p 2255" notes pekod@192.168.88.242::NetBackup/notes`
- **Copy file from NAS:**
  - `rsync -chavzP --stats -e 'ssh -p 2255' pekod@192.168.88.242::NetBackup/file ~/`
- **Sync with delete:**
  - `rsync -chavzP -r --delete -e "ssh -p 2255" .config/alacritty/alacritty.yml pekod@192.168.88.242::NetBackup`

---

## SCP

- **Secure copy to server:**
  - `scp -r /Users/mark/code/gant_chart/ root@192.168.1.22:/root/repos/gant-chart_bot`

---

## GPG & Password Management

- **Import GPG keys:**
  - `gpg --import public.gpg secret.gpg` — Import public and secret keys
- **Trust GPG key:**
  - `gpg --edit-key "onathema@gmail.com"` — Set trust level (e.g., 5)
- **Encrypt file:**
  - `gpg -e -a -r onathema@gmail.com file.csv` — Encrypt file with ASCII armor
- **Decrypt file:**
  - `gpg -d -o file.csv file.csv.asc` — Decrypt file
- **List keys:**
  - `gpg -K` — Show GPG keys

---

## Docker

- **Docker info:**
  - `docker info` — Show Docker engine details
- **Container management:**
  - `docker ps -a` — List all containers
  - `docker ps -q` — List container IDs only
  - `docker container stop [container ID]` — Stop container
  - `docker container start [container ID]` — Start container
  - `docker container restart [container ID]` — Restart container
  - `docker container rm [container ID]` — Remove container
  - `docker stop $(docker ps -a -q)` — Stop all containers
  - `docker rm $(docker ps -a -q)` — Remove all containers
- **Image management:**
  - `docker rmi $(docker images -q)` — Remove all images
- **Volume management:**
  - `docker volume ls` — List volumes
  - `docker volume ls -q` — List volume IDs only
  - `docker volume rm [volume ID]` — Remove volume
- **Disk usage:**
  - `docker system df` — Show disk usage
  - `docker system df -v` — Show detailed disk usage
- **Logs:**
  - `docker container logs [container ID]` — View container logs
- **Docker Compose:**
  - `docker-compose up -d` — Start services in detached mode
  - `docker compose -f metube.yml up` — Start using specific compose file
  - `docker-compose logs -f` — Follow logs
- **Build and run:**
  - `docker build -t [BOT_NAME] .` — Build Docker image
  - `docker run --env-file .env --name bill_bot -d bill_bot` — Run container with env file
  - **Note:** Ensure `BOT_TOKEN=` is defined in `.env`
- **Upgrade immich:**
  - `docker compose pull`
  - `docker compose up -d`
  - `docker image prune`

---

## macOS

- **Dock customization:**
  - `defaults write com.apple.dock autohide-time-modifier -float 0.15; killall Dock` — Adjust dock auto-hide speed
- **Reset Launchpad:**
  - `sudo find 2>/dev/null /private/var/folders/ -type d -name com.apple.dock.launchpad -exec rm -rf {} +; killall Dock`
- **Reset login items:**
  - `sfltool dumpbtm` — Reset login items and background tasks

---

## Git

- **Create repository on server:**
  - `mkdir /git/[category]/test.git && cd /git/[category]/test.git && git init --bare --shared`
- **Push to remote:**
  - `git push [category] [branch]` — Push to specific branch
  - `git push -u origin master` — Push and set upstream
- **Initialize local repo:**
  - `git init` — Create new repository
  - `git remote add origin <repository>` — Add remote repository
  - `git checkout master` — Switch to master branch
- **Update repo:**
  - `git pull` — Pull latest changes
- **View changes:**
  - `git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit` — Visual git log
- **Stash changes:**
  - `git stash` — Stash changes
  - `git stash pop` — Apply stashed changes
- **Configure git:**
  - `git config --global user.name "Thinker.What"`
  - `git config --global user.email "onathema@gmail.com"`
- **Create and commit:**
  - `touch README && git add README && git commit -m 'init README'`
- **Create zip from repo:**
  - `git archive [branch] | bzip2 > ~/Desktop/[project].zip`
- **Revert commit:**
  - `git revert` — Create commit to undo changes
- **Pull strategy:**
  - `git pull --no-ff origin main` — Pull with no fast-forward

---

## CLI Utilities & Commands

- **Search files:**
  - `grep "word" -r /path/` — Search for word in directory
- **Terminal settings:**
  - `infocmp` or `toe` — Check terminal mode
  - `echo $TERM` — Show terminal type
  - `TERM=xterm-256color` — Set terminal type
- **Network:**
  - `netstat -vanp tcp | grep 5` — Check port usage
  - `scutil --dns | grep 'nameserver\[[0-9]*\]'` — Check DNS
- **File system:**
  - `sudo su cd directory` — Access restricted directory
  - `du -shx` or `df -hl` — Check disk usage
  - `ls -a` — List all files (including hidden)
  - `pwd` — Print working directory
  - `bat` or `cat` — View file contents
  - `bat -d` — Show file changes
  - `tree` — Show directory tree
  - `stat -x file/directory` — Show file/directory stats
- **File changes:**
  - `find . -type f -mtime 0` — Find files modified in last 24 hours
  - `find . -type f -mtime 0 -print0 | xargs -0 ls -l` — List modified files
  - `find . -mtime 0 -exec ls -l {} \; | grep -v "total"` — List without total
- **File visibility:**
  - `chflags hidden file/folder` — Hide file/folder
  - `chflags nohidden file/folder` — Show file/folder
- **Command history:**
  - `history` — Show command history
  - `history -d [linenumber]` — Delete specific history entry
  - `history -p` or `history -c` — Clear history
- **Terminal font:**
  - `alacritty -o font.size=12.25` — Change Alacritty font size
- **Process control:**
  - `Ctrl+Z` — Suspend process
  - `fg` — Resume process
  - `Ctrl+C` or `q` — Kill process
- **File comparison:**
  - `diff file1 file2` — Compare files line by line
- **macOS quarantine:**
  - `xattr -dr com.apple.quarantine /Applications/Chromium.app` — Remove app quarantine
- **File permissions:**
  - `chmod 755 file` — Set full permissions
- **Terminal formatting:**
  - `echo -e "\e[3mfoo\e[23m"` — Test italic text
  - `echo -e "\e[1mbold\e[0m\n\e[3mitalic\e[0m\n\e[4munderline\e[0m\n\e[9mstrikethrough\e[0m"` — Test text styles
- **Trash cleanup:**
  - `sudo rm -r ./.Trash/*` — Force empty trash
- **Python version:**
  - `pyenv install 3.11` or `pyenv global 3.11` — Switch to Python 3.11
  - `echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc`
  - `echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc`
  - `exec zsh` or `source ~/.zshrc` — Reload shell
- **Archive:**
  - `tar -xvf` — Unarchive tar file
- **Oh My Zsh:**
  - `sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"` — Install Oh My Zsh
  - `git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions` — Install autosuggestions
  - `git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting` — Install syntax highlighting
  - `git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git $ZSH_CUSTOM/plugins/zsh-autocomplete` — Install autocomplete
- **Alpine Linux:**
  - `apk add shadow` — Add shadow package
  - `chsh -s $(which zsh)` — Set Zsh as default shell

---

## Fzf (Fuzzy Finder)

- **Install keybindings and completion:**
  - `$HOMEBREW_PREFIX/opt/fzf/install` — Apple Silicon
  - `(brew --prefix)/opt/fzf/install Ctrl+r (Ctrl+t)` — General
  - `(brew --prefix)/opt/fzf/install --tmux` — For tmux
  - `(brew --prefix)/opt/fzf/install --zsh` — For Zsh

---

## CUPS (Printing)

- **Edit configuration:**
  - `/etc/cups/cupsd.conf` — CUPS configuration file
- **Enable remote access:**
  - `cupsctl --remote-admin --remote-any --share-printers` — Allow remote printer access
- **Install print server:**
  - `brew install cups` — Install CUPS via Homebrew
- **Reference:**
  - [CUPS Documentation](https://help.ubuntu.ru/wiki/руководство_по_ubuntu_server/файловые_серверы/cups)

---

## Homebrew

- **Manage packages:**
  - `brew bundle dump` — Create Brewfile
  - `brew bundle install --file /path/tobrewfile` — Install packages from Brewfile
  - `brew bundle check` — Check for missing packages
- **List files with icons:**
  - `eza --icons -la -s=type` — Show files with icons

---

## FFmpeg

- **Common tasks:**
  - `ffmpeg -i input -c:v copy -c:a aac output` — Copy video, re-encode audio
  - `ffmpeg -i input -vcodec copy -acodec copy -c:s mov_text -map 0 -tag:v hvc1 output.mp4` — Copy video/audio, add subtitles
  - `ffmpeg -i input.mp3 -c:a aac -vn output.m4a` — Convert audio to M4A
  - `ffmpeg -i input -vn -acodec copy output.m4a` — Extract audio
  - `ffmpeg -i input -c:v libx265 -crf 28 -c:a aac -b:a 128k output.mp4` — Encode with HEVC
  - `ffmpeg -i input.mkv -vn -c:a libfdk_aac -b:a 256k output.m4a` — Convert audio to AAC
  - `ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac output.mp4` — Merge video and audio

---

## yt-dlp (YouTube Downloader)

- **Configuration:**
  - `mkdir -p ~/.config/youtube-dl/`
  - `echo "-o ~/Downloads/%(title)s.%(ext)s" > ~/.config/youtube-dl/config` — Set download path
- **Download options:**
  - `yt-dlp -f bestaudio --extract-audio --audio-format m4a --audio-quality 0 <Video-URL>` — Download audio as M4A
  - `yt-dlp -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best' <Video-URL>` — Download best video/audio
  - `yt-dlp "URL" --postprocessor-args "-c:v libx265 -preset ultrafast -crf 23 -tag:v hvc1 -c:a aac" --merge-output-format mp4` — Convert to HEVC
  - `yt-dlp "URL" --postprocessor-args "-c:v libx265 -preset fast -crf 15 -c:a opus -strict experimental -b:a 128k" --merge-output-format mp4` — Use Opus audio
- **Troubleshooting:**
  - `yt-dlp -f 299+251 --no-cache-dir URL` — Fix 403 forbidden
  - `yt-dlp --rm-cache-dir` — Clear cache
- **List formats:**
  - `yt-dlp <URL> -F` — Show available formats
  - `yt-dlp -f (number_audio+number_video) <URL>` — Download specific format
  - `--format bestvideo[ext=mp4]+bestaudio[ext=m4a]/bestvideo+bestaudio` — Preferred format
  - `--merge-output-format mp4` — Merge to MP4

---

## yandex-music downloader

`yandex-music-downloader --token "y0__xC9w6NqGN74BiCS4aWaFDCeovamCKRaNIYzXUtRhN6HjynGZMUN7plC" --quality 2 --url "https://music.yandex.ru/track/132687440?utm_source=web&utm_medium=copy_link"`

Запуск через `pdm run`
`pdm run yandex-music-downloader --token "y0__xC9w6NqGN74BiCS4aWaFDCeovamCKRaNIYzXUtRhN6HjynGZMUN7plC" --quality 2 --url "https://music.yandex.ru/track/132687440\?utm_source\=web\&utm_medium\=copy_link"`

## ImageMagick

- **Image manipulation:**
  - `convert testing.png -border 1x1 -bordercolor black result.png` — Add border
  - `convert testing.png -resize 1920 example.png` — Resize image
  - `convert testing.png -charcoal 2 example.png` — Apply charcoal effect
- **Batch processing:**
  - `for file in *.png; do convert $file -resize 1920 small-$file; done` — Batch resize
  - `mogrify -format heic *.jpg` — Batch convert to HEIC
  - `convert heic *.jpg` — Convert HEIC to JPG

---

## Exiftool

- **Modify metadata:**
  - `exiftool '-filemodifydate<datetimeoriginal' <file>` — Set file modification date from metadata

---

## RAR in Alpine Linux

- **Extract RAR:**
  - `apk add p7zip`
  - `7z e file.rar` — Extract RAR file

---

## grep

- **Поиск по файлам:** grep может искать заданный шаблон в одном или нескольких файлах.
- **Фильтрация вывода команд:** Результаты выполнения других команд можно передавать в  grep для поиска нужной информации.
- **Поддержка регулярных выражений:** Позволяет использовать сложные шаблоны для поиска, а не только точные совпадения.
- **Ключи командной строки:** grep имеет множество опций, таких как:
  - \-i: игнорировать регистр при поиске.
  - \-v: вывести строки, не соответствующие шаблону.
  - \-r или -R: рекурсивно искать во всех поддиректориях.
  - \-n: выводить номера строк, в которых найдено совпадение.
  - \-l: выводить только имена файлов, в которых найдено совпадение.
  - \-c: выводить количество совпадающих строк.

- **Примеры использования:**
  - `grep "error" logfile.txt`: Ищет строки, содержащие слово "error" в файле "logfile.txt".
  - `ls -l | grep "^d"`: Ищет только директории в выводе команды ls -l.
  - `grep -ri "example" .`: Рекурсивно ищет во всех файлах текущей директории и ее поддиректориях строки, содержащие "example", игнорируя регистр.
  - `grep -v "success" output.log`: Выводит все строки из output.log, которые не содержат "success".

grep и регулярные выражения:grep поддерживает широкий набор метасимволов и операторов для создания шаблонов. Вот некоторые примеры:

- ^: Совпадает с началом строки.
- $: Совпадает с концом строки.
- .: Совпадает с любым одиночным символом.
- \*: Совпадает с 0 или более вхождениями предыдущего символа.
- +: Совпадает с 1 или более вхождениями предыдущего символа.
- ?: Совпадает с 0 или 1 вхождением предыдущего символа.
- \[\]: Определяет набор символов, из которых должен соответствовать один символ.
- (): Группирует выражения.
- |: Означает логическое "или".

grep является одной из основных утилит в Linux и незаменим для работы с текстовыми данными.

---

## ZFS

- **Pool management:**
  - `sudo zfs set mountpoint=/mnt/zfspool zfspool` — Set mount point
  - `sudo zpool set autoexpand=on zfspool` — Enable auto-expansion
  - `zpool status datapool` — Check pool status
  - `zfs list` — List ZFS datasets
  - `df -h /mnt/mydata` — Show disk usage
- **Automount:**
  - Add to `/etc/udev/rules.d/90-zfs.rules`: `KERNEL=="sd*", ACTION=="add", RUN+="/usr/bin/zpool import zfspool"`
  - `sudo udevadm control --reload-rules` — Reload udev rules

