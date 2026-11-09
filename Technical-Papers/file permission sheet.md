## 1. View permissions and ownership

| Command | Purpose |
|---|---|
| `ls -l` | View file permissions |
| `ls -al` | View all files, including hidden files, with permissions |
| `ls -la` | Same as `ls -al` |
| `ls -ld folder/` | View the directory's own permissions |
| `ls -ald .*` | View hidden entries and their permissions |
| `stat file.txt` | Show detailed file metadata, permissions and ownership |
| `stat -c "%A %a %U %G %n" file` | Show permissions, numeric mode, owner, group and filename (GNU/Linux) |
| `namei -l /path/to/file` | Show permissions of each directory in a path (Linux) |
| `getfacl file.txt` | View ACL permissions |
| `id` | Show current user's UID and group IDs |
| `id manish` | Show another user's UID and group IDs |
| `groups` | Show current user's groups |
| `groups manish` | Show a user's groups |
| `whoami` | Show current username |
| `getent passwd manish` | Show user account entry (Linux) |
| `getent group developers` | Show group entry (Linux) |
| `sudo -l` | Show commands the current user may run with sudo |

## 2. Permission symbols and categories

### Permission symbols

| Symbol | Meaning |
|---|---|
| `r` | Read |
| `w` | Write |
| `x` | Execute |
| `-` | Permission not granted |
| `s` | SUID or SGID, depending on position |
| `t` | Sticky bit |

### Permission categories

| Category | Symbol | Meaning |
|---|---|---|
| Owner/User | `u` | The file's owner |
| Group | `g` | The file's group |
| Others | `o` | Everyone else |
| All | `a` | User, group and others |

Example:

```text
-rwxr-xr--
│││ │││ │││
│││ │││ └┴┴ Others: r--
│││ └┴┴ Group:  r-x
└┴┴ Owner:  rwx
```

The first character identifies the file type: `-` regular file, `d` directory, `l` symbolic link, `c` character device, `b` block device, `p` named pipe, and `s` socket.

## 3. Numeric permissions

Values are added together:

| Number | Symbol | Meaning |
|---:|---|---|
| 0 | `---` | No permissions |
| 1 | `--x` | Execute only |
| 2 | `-w-` | Write only |
| 3 | `-wx` | Write + execute |
| 4 | `r--` | Read only |
| 5 | `r-x` | Read + execute |
| 6 | `rw-` | Read + write |
| 7 | `rwx` | Read + write + execute |

Examples: `rwx = 4+2+1 = 7`; `rw- = 4+2 = 6`; `r-x = 4+1 = 5`.

## 4. `chmod` — change permissions using numeric mode

| Command | Result |
|---|---|
| `chmod 777 file` | Full permissions for everyone |
| `chmod 755 file` | Owner full; group and others read + execute |
| `chmod 750 file` | Owner full; group read + execute; others none |
| `chmod 700 file` | Owner full; group and others none |
| `chmod 644 file` | Owner read/write; group and others read |
| `chmod 640 file` | Owner read/write; group read; others none |
| `chmod 600 file` | Owner read/write only |
| `chmod 444 file` | Read-only for everyone |
| `chmod 400 file` | Owner read-only |
| `chmod 000 file` | No permissions for anyone |

Syntax:

```bash
chmod MODE FILE
chmod 755 script.sh
chmod 644 notes.txt
chmod 600 private.txt
```

## 5. `chmod` — change permissions using symbolic mode

| Command | Purpose |
|---|---|
| `chmod u+x file` | Add execute permission for owner |
| `chmod g+w file` | Add write permission for group |
| `chmod o+r file` | Add read permission for others |
| `chmod a+x file` | Add execute permission for all classes |
| `chmod u-w file` | Remove owner's write permission |
| `chmod g-r file` | Remove group's read permission |
| `chmod o-x file` | Remove others' execute permission |
| `chmod u=rwx file` | Set owner permissions exactly to `rwx` |
| `chmod g=rx file` | Set group permissions exactly to `r-x` |
| `chmod o=r file` | Set others permissions exactly to read |
| `chmod a=r file` | Set everyone to read-only |
| `chmod u=rw,g=r,o= file` | Set owner read/write, group read, others none |
| `chmod +x file` | Add execute permission to applicable classes |
| `chmod -x file` | Remove execute permission from applicable classes |

Operators: `+` adds, `-` removes, and `=` sets the specified permissions exactly.

## 6. Directory permissions

For directories, `r` allows listing names, `w` allows creating/deleting/renaming directory entries (normally together with `x`), and `x` allows traversal/access by name.

| Command | Purpose |
|---|---|
| `chmod 755 folder/` | Owner full; others list and traverse |
| `chmod 700 folder/` | Only owner has access |
| `chmod 750 folder/` | Owner full; group can list and traverse |
| `chmod 777 folder/` | Everyone has full directory permissions |
| `chmod u+x folder/` | Allow owner to traverse |
| `chmod g+w folder/` | Allow group to modify directory entries, subject to traversal and other rules |
| `chmod -R 755 folder/` | Apply mode recursively to directory contents |

**Important:** File permissions and parent-directory permissions are different. Deleting a file is generally controlled by write and execute permissions on its parent directory, not by the file's own write bit.

## 7. `chown` — change ownership

| Command | Purpose |
|---|---|
| `chown manish file` | Change owner to `manish` |
| `chown root file` | Change owner to `root` |
| `chown manish:dev file` | Change owner to `manish` and group to `dev` |
| `chown :dev file` | Change group only |
| `chown -R manish folder/` | Change owner recursively |
| `chown -R manish:dev folder/` | Change owner and group recursively |
| `chown -v manish file` | Display ownership changes |
| `chown --reference=ref.txt file` | Copy owner and group from a reference file (GNU/Linux) |

Examples:

```bash
sudo chown manish notes.txt
sudo chown manish:developers notes.txt
sudo chown -R manish:developers project/
```

Changing ownership commonly requires `sudo` or equivalent privileges.

## 8. `chgrp` — change group ownership

| Command | Purpose |
|---|---|
| `chgrp developers file` | Change file group to `developers` |
| `chgrp root file` | Change file group to `root` |
| `chgrp -R developers folder/` | Change group recursively |
| `chgrp -v developers file` | Display group changes |
| `chgrp --reference=ref.txt file` | Copy group from a reference file (GNU/Linux) |

## 9. Special permissions: SUID, SGID and sticky bit

| Special bit | Numeric value | Symbolic command | Meaning |
|---|---:|---|---|
| SUID | 4000 | `chmod u+s file` | Executable runs with the file owner's effective user ID |
| SGID | 2000 | `chmod g+s file` | Executable uses the file group's effective group ID; on directories, new items normally inherit the directory's group |
| Sticky bit | 1000 | `chmod +t folder/` | In a shared writable directory, users are restricted from deleting or renaming files they do not own (subject to privileged-user rules) |

Commands:

```bash
chmod 4755 file
chmod 2755 folder/
chmod 1777 folder/

chmod u+s file
chmod g+s folder/
chmod +t folder/

chmod u-s file
chmod g-s folder/
chmod -t folder/
```

A common sticky-bit example is `/tmp`. Inspect it with:

```bash
ls -ld /tmp
```

Special bits can display as lowercase `s`/`t` when the corresponding execute bit is set, or uppercase `S`/`T` when it is not.

## 10. `umask` — default permission mask

`umask` controls which permission bits are removed from permissions requested when new files and directories are created. Typical base modes are `666` for files and `777` for directories; applications can request different modes.

| Command | Purpose |
|---|---|
| `umask` | Display current umask |
| `umask -S` | Display symbolic umask |
| `umask 022` | Set umask to `022` in current shell |
| `umask 027` | Set umask to `027` |
| `umask 077` | Set umask to `077` |
| `umask 002` | Set umask to `002` |

Common results with the usual base modes:

| Umask | New file mode | New directory mode |
|---:|---:|---:|
| `000` | `666` | `777` |
| `022` | `644` | `755` |
| `027` | `640` | `750` |
| `077` | `600` | `700` |

Umask removes permissions; it does not grant permissions that the application did not request.

## 11. ACL — Access Control Lists

ACLs allow permissions for additional named users and groups beyond the traditional owner/group/others entries. On Linux, `getfacl` and `setfacl` are commonly provided by the `acl` package.

| Command | Purpose |
|---|---|
| `getfacl file` | View ACL entries |
| `setfacl -m u:john:rw file` | Give user `john` read/write ACL permissions |
| `setfacl -m g:dev:rwx file` | Give group `dev` read/write/execute ACL permissions |
| `setfacl -m u:john:r file` | Give user `john` read-only ACL permission |
| `setfacl -x u:john file` | Remove named user's ACL entry |
| `setfacl -x g:dev file` | Remove named group's ACL entry |
| `setfacl -b file` | Remove extended ACL entries |
| `setfacl -d -m g:dev:rwx folder/` | Set a default group ACL on a directory |
| `getfacl -R folder/` | View ACLs recursively |
| `setfacl -R -m u:john:rw folder/` | Apply an ACL recursively |

ACL masks can limit the effective permissions of named users, named groups and the owning group. Check `getfacl` output for `mask` and `effective` permissions.

## 12. Check whether a user/process can access a file

Shell tests:

```bash
test -r file && echo "Readable"
test -w file && echo "Writable"
test -x file && echo "Executable"

[ -r file ] && echo "Readable"
[ -w file ] && echo "Writable"
[ -x file ] && echo "Executable"
```

These test access for the current process, not an arbitrary username.

## 13. User and group inspection commands

| Command | Purpose |
|---|---|
| `whoami` | Current username |
| `id` | Current UID, primary group and supplementary groups |
| `id manish` | IDs and groups for `manish` |
| `groups` | Current user's groups |
| `groups manish` | Groups for `manish` |
| `getent passwd manish` | Look up user account (Linux) |
| `getent group developers` | Look up group (Linux) |
| `sudo -l` | Show current user's sudo permissions |

## 14. Practical examples

```bash
# View all files, including hidden files, with permissions
ls -al

# View a directory's own permissions
ls -ld project/

# Change a file's permissions
chmod 644 notes.txt

# Make a script executable by its owner/group/others as allowed by its other bits
chmod +x script.sh

# Set directory permissions
chmod 755 project/

# Change owner
sudo chown manish notes.txt

# Change group
sudo chgrp developers notes.txt

# Change owner and group
sudo chown manish:developers notes.txt

# Change ownership recursively
sudo chown -R manish:developers project/

# Set directories to 755 and regular files to 644 separately (GNU/Linux find)
find project/ -type d -exec chmod 755 {} \;
find project/ -type f -exec chmod 644 {} \;

# View detailed metadata
stat notes.txt

# Inspect permissions along a path (Linux)
namei -l /home/manish/project/notes.txt

# View ACL
getfacl notes.txt

# Check current umask
umask
```

**Caution:** Do not blindly use `chmod -R 777`. It makes files and directories broadly writable and executable. Also, the separate `find` commands above are a general example; some projects need executable files, private files or special directory permissions preserved.

## 15. Create and manage users and groups

### macOS

| Command | Purpose |
|---|---|
| `sudo dseditgroup -o create dev` | Create group `dev` |
| `sudo dseditgroup -o delete dev` | Delete group |
| `sudo dseditgroup -o edit -a manish -t user dev` | Add user to group |
| `sudo dseditgroup -o edit -d manish -t user dev` | Remove user from group |
| `sudo sysadminctl -addUser john -fullName "John" -password -` | Create user (prompts for password) |
| `sudo sysadminctl -deleteUser john` | Delete user |
| `sudo passwd john` | Change a user's password |

### Linux

| Command | Purpose |
|---|---|
| `sudo groupadd dev` | Create group |
| `sudo groupdel dev` | Delete group |
| `sudo useradd -m -s /bin/bash john` | Create user with a home directory |
| `sudo passwd john` | Set password |
| `sudo usermod -aG dev john` | Add user to group (append) |
| `sudo gpasswd -d john dev` | Remove user from group |
| `sudo usermod -g dev john` | Set primary group |
| `sudo userdel -r john` | Delete user and home directory |

## 16. Check users and groups

### macOS

| Command | Purpose |
|---|---|
| `dscl . -list /Users UniqueID \| awk '$2>=501'` | Custom users only (UID >= 501) |
| `dscl . -list /Groups PrimaryGroupID \| awk '$2>=501'` | Custom groups only (GID >= 501) |
| `dscl . -read /Groups/dev GroupMembership` | Members of a group |
| `dseditgroup -o read dev` | Full group details |
| `dseditgroup -o checkmember -m john dev` | Is `john` in `dev`? |
| `id john` | A user's UID, GID and groups |
| `groups john` | A user's groups |
| `dscl . -read /Users/john` | Full user record |

### Linux

| Command | Purpose |
|---|---|
| `getent passwd` | All users |
| `getent group` | All groups |
| `getent group dev` | One group and its members |
| `awk -F: '$3>=1000{print $1}' /etc/passwd` | Custom users only (UID >= 1000) |
| `awk -F: '$3>=1000{print $1}' /etc/group` | Custom groups only (GID >= 1000) |
| `id john` / `groups john` | A user's IDs and groups |
| `lastlog` | Last login of each user |

## 17. Quick revision — commands to memorize

```bash
# View permissions
ls -l
ls -al
ls -ld folder/
stat file
namei -l /path/to/file

# chmod: numeric and symbolic
chmod 755 file
chmod 644 file
chmod 600 file
chmod +x file
chmod u+x file
chmod g-w file
chmod -R 755 folder/

# Ownership and groups
chown user file
chown user:group file
chown -R user:group folder/
chgrp group file
chgrp -R group folder/

# Default permissions
umask
umask -S
umask 022

# ACL
getfacl file
setfacl -m u:user:rw file
setfacl -b file

# Special permissions
chmod 4755 file
chmod 2755 folder/
chmod 1777 folder/

# Check access
test -r file
test -w file
test -x file

# User and group information
whoami
id
groups
sudo -l

# Create / delete groups
sudo dseditgroup -o create dev            # macOS
sudo dseditgroup -o delete dev
sudo groupadd dev                         # Linux
sudo groupdel dev

# Create / delete users
sudo sysadminctl -addUser john -fullName "John" -password -   # macOS
sudo sysadminctl -deleteUser john
sudo useradd -m -s /bin/bash john         # Linux
sudo passwd john
sudo userdel -r john

# Add / remove user in group
sudo dseditgroup -o edit -a john -t user dev   # macOS add
sudo dseditgroup -o edit -d john -t user dev   # macOS remove
sudo usermod -aG dev john                      # Linux add
sudo gpasswd -d john dev                       # Linux remove

# Check users and groups (macOS)
dscl . -list /Users UniqueID | awk '$2>=501'          # custom users
dscl . -list /Groups PrimaryGroupID | awk '$2>=501'   # custom groups
dscl . -read /Groups/dev GroupMembership              # group members
dseditgroup -o read dev
dseditgroup -o checkmember -m john dev
id john
groups john

# Check users and groups (Linux)
getent passwd
getent group
getent group dev
awk -F: '$3>=1000{print $1}' /etc/passwd              # custom users
awk -F: '$3>=1000{print $1}' /etc/group               # custom groups
id john
groups john

# Verify ownership after setup
sudo chown john:dev project/
chmod 770 project/
ls -ld project/
```









[File_Permissions_Study_Guide.pdf](https://github.com/user-attachments/files/34509232/File_Permissions_Study_Guide.pdf)
