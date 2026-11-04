import pypandoc

content = r"""# Linux File & Directory Permissions — Complete Command Cheat Sheet (2026)

> Covers viewing permissions, hidden files, permission symbols, `chmod`, `chown`, `chgrp`, special bits, `umask`, ACLs, permission checks, and practical examples.
>
> **Platform note:** Most basic commands work on Linux and macOS. Some options shown (such as GNU `stat -c`, `namei`, `getfacl`, and `setfacl`) are Linux-specific or may need separate installation on macOS.

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

## 15. Quick revision — commands to memorize

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
```

## 16. Linux vs macOS notes

- Basic `ls`, `chmod`, `chown`, `chgrp`, `umask`, `stat` and shell permission tests are available on macOS.
- `stat -c` is GNU/Linux syntax. macOS `stat` uses different options, for example `stat -f "%Sp %Lp %Su %Sg %N" file`.
- `namei`, `getfacl` and `setfacl` are not standard macOS commands.
- macOS supports ACLs, but its ACL commands and syntax differ from Linux.
- For Linux-specific practice, use an Ubuntu VM or Linux machine.

"""

output_path = "/mnt/data/Linux_File_and_Directory_Permissions_Cheat_Sheet.md"
pypandoc.convert_text(content, "md", format="md", outputfile=output_path, extra_args=["--standalone"])
print(f"Created: {output_path}")
