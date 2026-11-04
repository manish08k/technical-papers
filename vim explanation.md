from pathlib import Path

content = r"""# Vim — Complete Explanation and Command Reference

This document explains Vim in simple language. It covers what Vim is, why it is useful, how its modes work, and how to use its important commands with examples.

## 1. What is Vim?

**Vim** stands for **Vi Improved**. It is a text editor that runs in the terminal. We can use it to create, read, and edit text files and source code.

Vim is commonly used by:
- Developers to edit source code and scripts.
- Linux administrators to edit configuration files.
- People working on remote servers through SSH.
- Anyone who wants to edit files quickly using the keyboard.

**Simple explanation:** Vim is a keyboard-based text editor that is especially useful when working in a terminal.

**Example:**

```bash
vim demo.txt
```

This opens `demo.txt` in Vim. If the file does not exist, Vim can create it when we save.

## 2. Why is Vim useful?

- It works directly in the terminal; a graphical desktop is not required.
- It is useful when connecting to remote Linux machines using SSH.
- Keyboard commands make many editing tasks quick.
- It provides powerful search and replace.
- It supports macros, which can repeat editing steps.
- It is available on many Unix-like systems.

**Simple explanation:** Vim is useful because we can edit files directly from the terminal, even on a remote server where a graphical editor may not be available.

## 3. Understanding Vim modes

Vim is called a **modal editor**. This means the keyboard performs different actions depending on the current mode.

| Mode | Purpose |
|---|---|
| Normal mode | Navigate through text and perform editing commands |
| Insert mode | Type and insert text |
| Visual mode | Select text |
| Command-line mode | Run commands such as save, quit, and replace |
| Replace mode | Overwrite existing characters while typing |

### Normal mode

Normal mode is the mode Vim starts in. We use it to move around and run commands.

Press `Esc` to return to Normal mode from another mode.

### Insert mode

Insert mode is used to type text.

- `i` — start typing before the cursor.
- `a` — start typing after the cursor.
- `o` — create a new line below and start typing.
- `O` — create a new line above and start typing.

Press `Esc` to leave Insert mode.

### Visual mode

Visual mode is used to select text.

- `v` — select characters.
- `V` — select complete lines.
- `Ctrl-v` — select a rectangular block of text.

### Command-line mode

Press `:` in Normal mode to enter a command. For example:

- `:w` — save.
- `:q` — quit.
- `:wq` — save and quit.

### Replace mode

Press `R` in Normal mode to overwrite existing text as you type. Press `Esc` to return to Normal mode.

**Simple explanation:** We use Insert mode to type, Normal mode to move and edit, Visual mode to select, and Command-line mode to run editor commands.

## 4. Opening and creating files

| Command | Purpose |
|---|---|
| `vim file.txt` | Open a file or create it when saved |
| `vim file1.txt file2.txt` | Open multiple files |
| `vim +10 file.txt` | Open a file at line 10 |
| `vim +/error file.txt` | Open a file at the first match for `error` |

**Example:**

```bash
vim notes.txt
```

This opens `notes.txt` in Vim.

## 5. Moving around in a file

These navigation keys are used in Normal mode.

| Key | Action |
|---|---|
| `h` | Move left |
| `j` | Move down |
| `k` | Move up |
| `l` | Move right |
| `w` | Move to the beginning of the next word |
| `b` | Move to the beginning of the previous word |
| `e` | Move to the end of the current or next word |
| `0` | Move to the first character position of the line |
| `^` | Move to the first non-blank character of the line |
| `$` | Move to the end of the line |
| `gg` | Go to the first line |
| `G` | Go to the last line |
| `10G` | Go to line 10 |
| `Ctrl-f` | Move one screen forward |
| `Ctrl-b` | Move one screen backward |

**Example:** Press `gg` to go to the beginning of the file and `G` to go to the end.

## 6. Inserting and editing text

| Command | Action |
|---|---|
| `i` | Insert before the cursor |
| `I` | Insert at the beginning of the line's text |
| `a` | Append after the cursor |
| `A` | Append at the end of the line |
| `o` | Open a new line below |
| `O` | Open a new line above |
| `r` | Replace one character |
| `R` | Enter Replace mode |
| `J` | Join the current line with the next line |

**Example:** Move the cursor to a line and press `A` to add text at the end of that line.

## 7. Deleting, copying and pasting

| Command | Action |
|---|---|
| `x` | Delete the character under the cursor |
| `X` | Delete the character before the cursor |
| `dd` | Delete the current line |
| `3dd` | Delete three lines |
| `dw` | Delete from the cursor to the next word boundary |
| `D` | Delete from the cursor to the end of the line |
| `yy` | Copy (yank) the current line |
| `3yy` | Copy three lines |
| `yw` | Copy a word movement from the cursor |
| `p` | Paste after the cursor, or below for line-wise text |
| `P` | Paste before the cursor, or above for line-wise text |

**Simple explanation:** In Vim, `d` is used to delete, `y` is used to copy, and `p` is used to paste.

**Example:**

```text
dd  → delete the current line
yy  → copy the current line
p   → paste the copied line
```

## 8. Changing text, undo and redo

| Command | Action |
|---|---|
| `cw` | Change text from the cursor through the end of the word |
| `ciw` | Change the word under the cursor |
| `cc` | Change the entire line |
| `C` | Change from the cursor to the end of the line |
| `u` | Undo the last change |
| `Ctrl-r` | Redo an undone change |
| `.` | Repeat the last change |

**What does `ciw` mean?**

- `c` means change.
- `i` means inside.
- `w` means word.

So, `ciw` deletes the word under the cursor and enters Insert mode so we can type a replacement.

## 9. Selecting text with Visual mode

| Command | Action |
|---|---|
| `v` | Start character-wise selection |
| `V` | Start line-wise selection |
| `Ctrl-v` | Start block-wise selection |
| `y` | Copy the selected text |
| `d` | Delete the selected text |
| `>` | Indent the selected text |
| `<` | Remove one level of indentation |

**Example:** Press `V`, move up or down to select lines, and press `>` to indent them.

## 10. Searching for text

| Command | Action |
|---|---|
| `/word` | Search forward for `word` |
| `?word` | Search backward for `word` |
| `n` | Move to the next search match |
| `N` | Move to the previous search match |
| `*` | Search forward for the word under the cursor |
| `#` | Search backward for the word under the cursor |

**Example:**

```vim
/error
```

Press Enter to search for `error`. Use `n` to move to the next match and `N` to move to the previous match.

## 11. Replacing text

Vim uses the substitute command to replace text.

| Command | Action |
|---|---|
| `:s/old/new/` | Replace the first match on the current line |
| `:s/old/new/g` | Replace all matches on the current line |
| `:%s/old/new/g` | Replace all matches in the file |
| `:%s/old/new/gc` | Ask for confirmation before each replacement |
| `:10,20s/old/new/g` | Replace matches between lines 10 and 20 |

**Example:**

```vim
:%s/apple/orange/gc
```

This searches the whole file, replaces `apple` with `orange`, and asks before each replacement.

**What do the symbols mean?**
- `%` means the whole file.
- `s` means substitute.
- `g` means all matches on each line.
- `c` means ask for confirmation.

## 12. Saving and quitting

| Command | Action |
|---|---|
| `:w` | Save the file |
| `:w filename` | Save using another filename |
| `:q` | Quit if there are no unsaved changes |
| `:wq` | Save and quit |
| `:x` | Save if changed and quit |
| `:q!` | Quit without saving changes |
| `:wqa` | Save all open files and quit all windows |

**Simple explanation:** Use `:w` to save, `:q` to quit, and `:wq` to save and quit. Be careful with `:q!` because it discards unsaved changes.

## 13. Buffers, windows and tabs

Vim uses three concepts to organize editing.

- **Buffer:** The text loaded into memory for a file.
- **Window:** A view that displays a buffer.
- **Tab page:** A collection of windows.

A buffer can exist without being visible. A window displays a buffer, and more than one window can display the same buffer.

### Buffer commands

| Command | Action |
|---|---|
| `:ls` | List open buffers |
| `:e file.txt` | Open a file in the current window |
| `:bn` | Go to the next buffer |
| `:bp` | Go to the previous buffer |
| `:bd` | Delete the current buffer from the buffer list |

### Window commands

| Command | Action |
|---|---|
| `:split` | Create a horizontal split |
| `:vsplit` | Create a vertical split |
| `Ctrl-w w` | Switch to another window |
| `Ctrl-w h` | Move to the window on the left |
| `Ctrl-w j` | Move to the window below |
| `Ctrl-w k` | Move to the window above |
| `Ctrl-w l` | Move to the window on the right |
| `:close` | Close the current window |

### Tab commands

| Command | Action |
|---|---|
| `:tabnew` | Open a new tab page |
| `:tabnext` or `gt` | Move to the next tab page |
| `:tabprevious` or `gT` | Move to the previous tab page |
| `:tabclose` | Close the current tab page |

**Simple explanation:** A buffer is the file content, a window is the view of that content, and a tab page can contain multiple windows.

## 14. Registers and macros

### Registers

A register is a place where Vim stores text that we copy or delete. We can use registers to paste stored text later.

| Command | Action |
|---|---|
| `:reg` | Display register contents |
| `"ayy` | Copy the current line into register `a` |
| `"ap` | Paste the contents of register `a` |
| `"+y` | Copy selected text to the system clipboard, if clipboard support is available |
| `"+p` | Paste from the system clipboard, if clipboard support is available |

### Macros

A macro records a sequence of keystrokes so that we can repeat the same editing task.

| Command | Action |
|---|---|
| `qa` | Start recording into register `a` |
| `q` | Stop recording |
| `@a` | Run the macro stored in register `a` |
| `@@` | Run the last executed macro again |
| `10@a` | Run register `a`'s macro ten times |

**Simple explanation:** Registers store text. Macros store editing actions. Both help us avoid repeating work manually.

## 15. Indentation and formatting

| Command | Action |
|---|---|
| `>>` | Indent the current line |
| `<<` | Remove one level of indentation |
| `==` | Automatically indent the current line |
| `gg=G` | Re-indent the entire file |
| `:set number` | Show line numbers |
| `:set nonumber` | Hide line numbers |

**Example:** Use `gg=G` to ask Vim to re-indent the entire file according to its indentation settings and file type.

## 16. Useful information and diagnostic commands

These commands help us inspect Vim and understand how a file is being handled.

| Command | What it shows | Why it is useful |
|---|---|---|
| `:messages` | Recent Vim messages | Check warnings, errors and command output |
| `:scriptnames` | Scripts loaded in the current session | Check which configuration and plugin scripts were loaded |
| `:version` | Version, build details and supported features | Check the installed Vim version and available features |
| `:set fileformat?` | Current line-ending format | Check whether the file uses Unix or DOS/Windows line endings |
| `:set fileencoding?` | Current file character encoding | Check whether the file uses an encoding such as UTF-8 |
| `:set number?` | Whether line numbers are enabled | Check the current line-number setting |
| `:set paste?` | Whether paste mode is enabled | Check the current paste setting |
| `:pwd` | Vim's current working directory | See which directory Vim is using |
| `:echo $MYVIMRC` | Path stored in the `MYVIMRC` environment variable | Help locate the Vim configuration file when set |

**Important difference:**
- `fileformat` is about line endings, such as `unix` (LF) or `dos` (CRLF).
- `fileencoding` is about how characters are encoded, such as UTF-8.

These are two different file properties.

## 17. Vim configuration

Vim settings can be saved in a configuration file so they are applied whenever Vim starts.

Common configuration files:
- Vim: `~/.vimrc`
- Neovim with Lua: `~/.config/nvim/init.lua`
- Neovim with Vimscript: `~/.config/nvim/init.vim`

Example Vim configuration:

```vim
set number
set relativenumber
set tabstop=4
set shiftwidth=4
set expandtab
set ignorecase
set smartcase
syntax on
```

What these settings do:

| Setting | Purpose |
|---|---|
| `number` | Show line numbers |
| `relativenumber` | Show relative line numbers |
| `tabstop=4` | Display a tab using a width of four spaces |
| `shiftwidth=4` | Use four spaces for indentation operations |
| `expandtab` | Insert spaces instead of tab characters |
| `ignorecase` | Ignore case in searches |
| `smartcase` | Make searches case-sensitive when uppercase letters are used |
| `syntax on` | Enable syntax highlighting where supported |

## 18. What is Neovim?

**Neovim** is a modern, community-driven fork of Vim. It keeps the familiar modal editing approach and many Vim commands, while providing modern APIs and extensibility. It also supports Lua for configuration.

| Vim | Neovim |
|---|---|
| Original improved version of Vi | Community-driven fork of Vim |
| Commonly configured using `~/.vimrc` | Commonly configured using `init.lua` |
| Uses Vimscript for configuration and scripting | Supports Lua as well as Vimscript |
| Widely available on Unix-like systems | Focuses on modern extensibility and APIs |

**Simple explanation:** Neovim is a modern alternative to Vim. If we understand Vim's modes and commands, much of that knowledge also works in Neovim.

## 19. Vim and Linux: practical uses

Vim is useful in everyday Linux work.

**Edit a configuration file:**

```bash
vim ~/.bashrc
```

**Edit a system configuration file:**

```bash
sudo vim /etc/hosts
```

Administrative access may be required to edit system files. Only save changes when you understand their effect.

**Open a log file:**

```bash
vim /var/log/syslog
```

The log file may require permissions, and the path can differ between Linux distributions.

**Simple explanation:** Vim lets us edit configuration files, scripts and logs directly from the terminal. This is especially useful when working on a Linux server over SSH.

## 20. Vim help and troubleshooting

| Command | Action |
|---|---|
| `:help` | Open Vim's built-in help |
| `:help :w` | Read help for the save command |
| `:help motion` | Read help about motions |
| `:messages` | Review recent messages |
| `:checkhealth` | Run health checks in supported Neovim versions |

If Vim seems stuck in a mode, press `Esc` to return to Normal mode. If a command is unfamiliar, use `:help` followed by the command or topic.

**Swap-file warning:** Vim may create a swap file while editing. If a warning appears, check whether the same file is open in another Vim session and whether unsaved work can be recovered. Do not delete the swap file without checking.

## 21. Vim vs a regular text editor

| Vim | Typical graphical text editor |
|---|---|
| Primarily keyboard-driven | Often uses both keyboard and mouse |
| Uses different modes | Usually has one main editing mode |
| Works directly in a terminal | Usually runs in a graphical interface |
| Powerful command combinations | Often relies on menus, shortcuts and toolbar actions |
| Very useful over SSH | May require a graphical environment or remote desktop |

Neither approach is best for every situation. The right editor depends on the task and the user's preference.

## 22. Quick command reference

| Goal | Command |
|---|---|
| Open a file | `vim file.txt` |
| Enter Insert mode | `i` |
| Return to Normal mode | `Esc` |
| Save | `:w` |
| Quit | `:q` |
| Save and quit | `:wq` |
| Quit without saving | `:q!` |
| Move left/down/up/right | `h`, `j`, `k`, `l` |
| Next word | `w` |
| Previous word | `b` |
| Beginning of line | `0` |
| End of line | `$` |
| First line | `gg` |
| Last line | `G` |
| Delete line | `dd` |
| Copy line | `yy` |
| Paste | `p` |
| Undo | `u` |
| Redo | `Ctrl-r` |
| Search forward | `/word` |
| Next search match | `n` |
| Select characters | `v` |
| Select lines | `V` |
| Change inner word | `ciw` |
| Replace throughout file | `:%s/old/new/g` |
| Show line numbers | `:set number` |
| Open help | `:help` |

