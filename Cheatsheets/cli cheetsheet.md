
# CLI (Command Line Interface) – Complete Command Reference

## 1. TERMINAL & SHELL

```bash
whoami
id
hostname
uname
uname -a
uname -s
uname -r
uname -m
echo $SHELL
ps $$
ps -p $$
cat /etc/shells
clear
history
history 10
!!
!NUMBER
```

## 2. MANUAL & HELP

```bash
man COMMAND
COMMAND --help
help
type COMMAND
which COMMAND
whereis COMMAND
whatis COMMAND
apropos KEYWORD
```

## 3. NAVIGATION & PATHS

```bash
pwd
cd
cd ~
cd /
cd ..
cd .
cd -
cd DIRECTORY
ls
ls -l
ls -a
ls -la
ls -lh
ls -lt
ls -ltr
ls -R
ls -S
ls -lah
tree
tree -L 2
find .
realpath FILE
dirname PATH
basename PATH
```

## 4. CREATE FILES & DIRECTORIES

```bash
touch FILE
mkdir DIRECTORY
mkdir -p parent/child
mkdir -v DIRECTORY
mktemp
mktemp -d
```

## 5. COPY, MOVE & RENAME

```bash
cp FILE DESTINATION
cp FILE1 FILE2 DIRECTORY
cp -r DIRECTORY DESTINATION
cp -a DIRECTORY DESTINATION
cp -v FILE DESTINATION

mv FILE DESTINATION
mv OLD_NAME NEW_NAME
mv -i FILE DESTINATION
mv -f FILE DESTINATION
mv -v FILE DESTINATION
```

## 6. DELETE FILES & DIRECTORIES

```bash
rm FILE
rm -i FILE
rm -f FILE
rm -r DIRECTORY
rm -rf DIRECTORY
rmdir DIRECTORY
rmdir -p DIRECTORY
```

## 7. READ FILES

```bash
cat FILE
cat FILE1 FILE2
cat -n FILE
less FILE
more FILE
head FILE
head -n 10 FILE
tail FILE
tail -n 10 FILE
tail -f FILE
tail -F FILE
nl FILE
tac FILE
```

## 8. SEARCH FILES & CONTENT

```bash
find . -name "FILE"
find . -iname "FILE"
find . -type f
find . -type d
find . -size +100M
find . -mtime -7
find . -empty
find . -name "*.log"
find . -type f -delete

grep "WORD" FILE
grep -i "WORD" FILE
grep -n "WORD" FILE
grep -v "WORD" FILE
grep -r "WORD" DIRECTORY
grep -rn "WORD" DIRECTORY
grep -l "WORD" FILE
grep -c "WORD" FILE
grep -w "WORD" FILE
grep -E "PATTERN" FILE
```

## 9. TEXT PROCESSING

```bash
sort FILE
sort -r FILE
sort -n FILE
sort -u FILE
uniq FILE
uniq -c FILE
uniq -d FILE
cut -d',' -f1 FILE
cut -c1-10 FILE
tr 'a-z' 'A-Z'
tr -d 'CHAR'
rev FILE
paste FILE1 FILE2
join FILE1 FILE2
comm FILE1 FILE2
```

## 10. WORD COUNT & STATISTICS

```bash
wc FILE
wc -l FILE
wc -w FILE
wc -c FILE
wc -m FILE
du -sh DIRECTORY
du -h FILE
du -ah DIRECTORY
du -sh *
df -h
df -T
```

## 11. PIPES & REDIRECTION

```bash
COMMAND1 | COMMAND2
COMMAND1 | COMMAND2 | COMMAND3

COMMAND > FILE
COMMAND >> FILE
COMMAND < FILE
COMMAND 2> ERROR_FILE
COMMAND 2>> ERROR_FILE
COMMAND &> OUTPUT_FILE
COMMAND > FILE 2>&1
COMMAND1 | tee FILE
COMMAND1 | tee -a FILE
COMMAND1 | xargs COMMAND
```

## 12. FILE PERMISSIONS

```bash
ls -l
stat FILE
chmod 755 FILE
chmod 644 FILE
chmod 700 FILE
chmod 777 FILE
chmod +x FILE
chmod -x FILE
chmod u+x FILE
chmod g+w FILE
chmod o-r FILE
chmod -R 755 DIRECTORY
chmod --reference=FILE1 FILE2
```

### Ownership

```bash
chown USER FILE
chown USER:GROUP FILE
chown -R USER:GROUP DIRECTORY
chgrp GROUP FILE
chgrp -R GROUP DIRECTORY
```

## 13. SUDO & USERS

```bash
sudo COMMAND
sudo -i
sudo -s
sudo -u USER COMMAND
sudo whoami

whoami
id
groups
users
who
w
su USER
passwd
```

## 14. PROCESSES

```bash
ps
ps aux
ps -ef
ps -u USER
ps -p PID
ps -l
ps -f
ps -o pid,ppid,cmd
ps -p PID -o pid,ppid,cmd

top
htop

pgrep PROCESS
pgrep -a PROCESS
pidof PROCESS
pstree
pstree -p
```

## 15. PROCESS CONTROL

```bash
kill PID
kill -15 PID
kill -9 PID
kill -2 PID
kill -l
killall PROCESS
pkill PROCESS
pkill -f PATTERN

COMMAND &
jobs
jobs -l
fg
fg %1
bg
bg %1
nohup COMMAND &
```

## 16. CPU & MEMORY

```bash
top
htop
free
free -h
vmstat
vmstat 1
uptime
lscpu
nproc
```

## 17. DISK & STORAGE

```bash
df
df -h
df -T
du -sh DIRECTORY
du -h FILE
du -ah DIRECTORY
du -sh *
lsblk
lsblk -f
mount
umount DEVICE
```

## 18. NETWORKING

```bash
ip addr
ip link
ip route
ifconfig
hostname -I
hostname -i

ping google.com
ping -c 4 google.com

curl URL
curl -I URL
curl -L URL
wget URL

ss -tulnp
ss -tulpn
ss -tan
netstat -tulnp
lsof -i
lsof -i :8000

nslookup google.com
dig google.com
host google.com
traceroute google.com
```

## 19. SSH & REMOTE CONNECTIONS

```bash
ssh USER@HOST
ssh -p PORT USER@HOST
ssh-keygen
ssh-copy-id USER@HOST
ssh-add KEY_FILE
ssh-add -l

scp FILE USER@HOST:/PATH
scp USER@HOST:/PATH FILE
scp -r DIRECTORY USER@HOST:/PATH

rsync -av SOURCE DESTINATION
rsync -avz SOURCE USER@HOST:/PATH
rsync -av --delete SOURCE DESTINATION
```

## 20. ENVIRONMENT VARIABLES

```bash
env
printenv
printenv PATH
echo $PATH
echo $HOME
echo $USER
echo $SHELL

export NAME=value
unset NAME
export PATH="$PATH:/NEW/PATH"
```

## 21. PATH & EXECUTABLES

```bash
which python
which node
which code
whereis python
type python
command -v python
echo $PATH
```

## 22. PACKAGE MANAGEMENT – UBUNTU

```bash
sudo apt update
sudo apt upgrade
sudo apt full-upgrade
sudo apt install PACKAGE
sudo apt remove PACKAGE
sudo apt purge PACKAGE
sudo apt autoremove
sudo apt search PACKAGE
sudo apt show PACKAGE
sudo apt list --installed
sudo apt clean
```

## 23. PACKAGE MANAGEMENT – MAC (HOMEBREW)

```bash
brew --version
brew update
brew upgrade
brew install PACKAGE
brew uninstall PACKAGE
brew reinstall PACKAGE
brew search PACKAGE
brew info PACKAGE
brew list
brew list --versions
brew cleanup
brew doctor
```

## 24. ARCHIVES & COMPRESSION

```bash
tar -cvf archive.tar DIRECTORY
tar -xvf archive.tar
tar -czvf archive.tar.gz DIRECTORY
tar -xzvf archive.tar.gz
tar -tvf archive.tar
tar -czf archive.tar.gz FILE

gzip FILE
gunzip FILE.gz
zip archive.zip FILE
zip -r archive.zip DIRECTORY
unzip archive.zip
unzip -l archive.zip
```

## 25. DATE & TIME

```bash
date
date +"%Y-%m-%d"
date +"%H:%M:%S"
cal
uptime
timedatectl
```

## 26. SYSTEM INFORMATION

```bash
uname -a
hostname
hostnamectl
lscpu
lsmem
free -h
lsblk
lspci
lsusb
arch
getconf LONG_BIT
```

## 27. FILE LINKS

```bash
ln FILE LINK
ln -s TARGET LINK
readlink LINK
readlink -f FILE
stat FILE
file FILE
```

## 28. SHELL HISTORY & SHORTCUTS

```bash
history
history 20
history -c
!!
!NUMBER
!COMMAND

Ctrl + C
Ctrl + D
Ctrl + Z
Ctrl + R
Ctrl + L
Tab
Arrow Up
Arrow Down
```

## 29. BASH COMMANDS

```bash
bash
bash SCRIPT.sh
bash -x SCRIPT.sh
source FILE
source ~/.bashrc
. FILE

alias
alias ll='ls -lah'
unalias ll

echo "Hello"
printf "Hello\n"
read VARIABLE
```

## 30. AWK

```bash
awk '{print $1}' FILE
awk '{print $NF}' FILE
awk '{print NR, $0}' FILE
awk -F',' '{print $1}' FILE
awk 'NR==5' FILE
awk 'NR>=10 && NR<=20' FILE
awk '/ERROR/' FILE
awk '{count++} END {print count}' FILE
```

## 31. SED

```bash
sed 's/OLD/NEW/' FILE
sed 's/OLD/NEW/g' FILE
sed -n '1,10p' FILE
sed -n '5p' FILE
sed '/WORD/d' FILE
sed -i 's/OLD/NEW/g' FILE
sed -i.bak 's/OLD/NEW/g' FILE
```

## 32. XARGS

```bash
xargs COMMAND
find . -name "*.log" | xargs rm
find . -name "*.txt" | xargs wc -l
cat FILE | xargs
echo "a b c" | xargs
```

## 33. PROCESS & PORT MANAGEMENT

```bash
lsof -i :8000
lsof -i :5432
ps aux | grep PROCESS
ps -ef | grep PROCESS
pgrep -a PROCESS
fuser -n tcp 8000
fuser -k 8000/tcp

python3 -m http.server 8000
python3 -m http.server 90
```

## 34. PYTHON ENVIRONMENT

```bash
python3 --version
python3 -m venv venv
source venv/bin/activate
deactivate

pip install PACKAGE
pip uninstall PACKAGE
pip list
pip freeze
pip freeze > requirements.txt
pip install -r requirements.txt
pip show PACKAGE
```

## 35. NODE.JS & NPM

```bash
node --version
npm --version
npm init
npm init -y
npm install
npm install PACKAGE
npm uninstall PACKAGE
npm update
npm list
npm list -g
npm run dev
npm run build
npm start
npx COMMAND
```

## 36. GIT COMMANDS

```bash
git --version
git init
git clone URL
git status
git add .
git commit -m "MESSAGE"
git log --oneline
git branch
git switch BRANCH
git switch -c BRANCH
git checkout BRANCH
git merge BRANCH
git fetch
git pull
git push
git push -u origin main
git remote -v
git stash
git stash pop
git diff
git diff --staged
git reset --soft HEAD~1
git reset --hard HEAD
git revert COMMIT_ID
git reflog
```

## 37. SYMBOLS & WILDCARDS

| Symbol | Meaning |
|---|---|
| `.` | Current directory |
| `..` | Parent directory |
| `~` | Home directory |
| `/` | Root directory |
| `-` | Previous directory in `cd -` |
| `*` | Matches multiple characters |
| `?` | Matches one character |
| `|` | Pipe |
| `>` | Redirect output |
| `>>` | Append output |
| `<` | Input redirection |
| `&&` | Run next command if previous succeeds |
| `||` | Run next command if previous fails |
| `;` | Run commands sequentially |
| `&` | Run command in background |
| `$` | Variable expansion |
| `\` | Escape character |

## 38. IMPORTANT CLI PRACTICE

- [ ] Navigate directories using `cd`, `pwd`, and `ls`.
- [ ] Create files and directories using `touch` and `mkdir`.
- [ ] Copy, move, rename and delete files.
- [ ] Read files using `cat`, `less`, `head`, and `tail`.
- [ ] Search using `grep` and `find`.
- [ ] Understand absolute and relative paths.
- [ ] Understand file permissions using `chmod` and `chown`.
- [ ] Understand pipes and redirection.
- [ ] Extract process IDs using `ps`, `grep`, `awk`, and `xargs`.
- [ ] Identify parent and child processes.
- [ ] Start and stop processes.
- [ ] Identify processes running on specific ports.
- [ ] Check CPU, memory and disk usage.
- [ ] Check IP addresses and network connections.
- [ ] Connect to remote machines using SSH.
- [ ] Understand shell variables and PATH.
- [ ] Practice `sed` and `awk`.
- [ ] Learn terminal shortcuts.
- [ ] Practice Bash scripting.

## 39. DANGEROUS COMMANDS

**Warning:** These commands can permanently delete files or terminate processes.

```bash
rm -rf DIRECTORY
sudo rm -rf DIRECTORY
chmod -R 777 DIRECTORY
kill -9 PID
killall PROCESS
pkill -9 PROCESS
```

## 40. USEFUL DAILY COMMAND COMBINATIONS

```bash
# Current directory
pwd

# List all files with details
ls -lah

# Find a file
find . -name "FILE"

# Search text recursively
grep -rn "WORD" .

# Find process
ps aux | grep PROCESS

# Find process using a port
lsof -i :8000

# Show disk usage
df -h

# Show directory size
du -sh DIRECTORY

# Show memory
free -h

# Show current shell
echo $SHELL

# Show PATH
echo $PATH

# Show last 20 commands
history 20

# Follow logs
tail -f FILE

# Count lines
wc -l FILE

# Find largest files in current directory
du -ah . | sort -rh | head -n 10

# Check network
ping -c 4 google.com

# Show listening ports
ss -tulnp
```

---

**Note:** Some commands are Linux-specific. On macOS, commands such as `lspci`, `apt`, `free`, and `ss` may not be available by default. Use macOS equivalents where needed.
