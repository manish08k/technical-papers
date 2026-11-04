
## Slide 1 — What is Vim?

**Vim** stands for **Vi Improved**. It is a terminal-based, keyboard-driven text editor used to create and edit files.

Developers and system administrators use Vim to:
- Edit source code and scripts.
- Modify Linux configuration files.
- Work on remote servers through SSH.
- Search and replace text efficiently.

**Presenter explanation:**  
“Vim is a text editor that lets us work mainly with the keyboard. It is especially useful when we are working in a terminal or connected to a remote Linux server.”

## Slide 2 — Why is Vim different?

Vim is a **modal editor**. This means the keyboard has different functions depending on the mode.

| Mode | Purpose |
|---|---|
| Normal mode | Navigate and perform editing operations |
| Insert mode | Type and insert text |
| Visual mode | Select text |
| Command-line mode | Run commands such as save, quit and search-and-replace |
| Replace mode | Overwrite existing characters |

**Presenter explanation:**  
“In a regular text editor, we usually type directly into the document. In Vim, we first choose what we want to do. For example, we use Insert mode to type and Normal mode to navigate or edit.”

**Demonstration:** Open a file with `vim demo.txt`, press `i` to type, press `Esc` to return to Normal mode, then enter `:wq` to save and quit.

## Slide 3 — Basic navigation

Vim uses keyboard keys to move around the file.

| Key | Action |
|---|---|
| `h` | Move left |
| `j` | Move down |
| `k` | Move up |
| `l` | Move right |
| `w` | Move to the next word |
| `b` | Move to the previous word |
| `0` | Move to the beginning of the line |
| `$` | Move to the end of the line |
| `gg` | Go to the first line |
| `G` | Go to the last line |

**Presenter explanation:**  
“These keys let us move through a file without using the mouse. For example, `gg` takes us to the top of the file and `G` takes us to the bottom.”

## Slide 4 — Common editing commands

| Command | Action |
|---|---|
| `i` | Insert text before the cursor |
| `a` | Insert text after the cursor |
| `o` | Create a new line below |
| `O` | Create a new line above |
| `x` | Delete a character |
| `dd` | Delete the current line |
| `yy` | Copy the current line |
| `p` | Paste after or below |
| `u` | Undo |
| `Ctrl-r` | Redo |
| `.` | Repeat the last change |

**Presenter explanation:**  
“Vim commands are short. `dd` deletes a line, `yy` copies a line, and `p` pastes it. If we make a mistake, `u` undoes the change.”

## Slide 5 — A useful Vim command pattern

Many Vim commands combine an **operator** with a **motion** or **text object**.

```text
[count] + [operator] + [motion or text object]
```

| Part | Meaning | Examples |
|---|---|---|
| Count | How many times | `3` |
| Operator | What action to perform | `d` delete, `c` change, `y` copy |
| Motion | Where the action applies | `w`, `$`, `}` |
| Text object | A structured text region | `iw`, `i"`, `i(` |

Examples:
- `dw` — delete from the cursor to the next word boundary.
- `3dd` — delete three lines.
- `ciw` — change the word under the cursor.
- `yy` — copy the current line.

**Presenter explanation:**  
“Instead of memorizing a separate command for every task, we can combine an action with a movement. This is one of the ideas that makes Vim powerful.”

## Slide 6 — Search and replace

Vim can search for text and replace it.

| Command | Action |
|---|---|
| `/error` | Search forward for `error` |
| `n` | Go to the next match |
| `N` | Go to the previous match |
| `:%s/old/new/g` | Replace all matches in the file |
| `:%s/old/new/gc` | Ask before each replacement |

**Presenter explanation:**  
“Suppose a variable name appears many times in a file. We can use search-and-replace to update it instead of changing each occurrence manually.”

Example:

```vim
:%s/old_name/new_name/gc
```

The `g` flag replaces every match on each line, and `c` asks for confirmation.

## Slide 7 — Saving and exiting

| Command | Action |
|---|---|
| `:w` | Save the file |
| `:q` | Quit if there are no unsaved changes |
| `:wq` | Save and quit |
| `:q!` | Quit without saving changes |
| `:x` | Save if changed and quit |

**Presenter explanation:**  
“After editing, we need to save our changes. `:w` saves, `:q` exits, and `:wq` does both. `:q!` exits without saving, so use it only when we intentionally want to discard changes.”

## Slide 8 — Buffers, windows and tabs

These three terms describe how Vim organizes files and views.

| Term | Meaning |
|---|---|
| Buffer | The text loaded in memory |
| Window | A view displaying a buffer |
| Tab page | A collection of windows |

Useful commands:

| Command | Action |
|---|---|
| `:ls` | List open buffers |
| `:bn` | Move to the next buffer |
| `:bp` | Move to the previous buffer |
| `:split` | Create a horizontal split |
| `:vsplit` | Create a vertical split |
| `Ctrl-w w` | Move between windows |
| `:tabnew` | Create a new tab page |
| `gt` | Move to the next tab page |

**Presenter explanation:**  
“A buffer is the content being edited. A window is where we see that content. A tab page can contain multiple windows. This is slightly different from the file-tab system used by many graphical editors.”

## Slide 9 — Useful diagnostic commands

These commands help us inspect Vim's state and configuration.

| Command | What it shows | When it is useful |
|---|---|---|
| `:messages` | Recent messages from Vim | Check warnings, errors or command output |
| `:scriptnames` | Scripts and configuration files loaded in the current session | Investigate which configuration or plugin scripts were loaded |
| `:version` | Vim version, build information and supported features | Check the installed version and whether features such as clipboard support are available |
| `:set fileformat?` | Current file line-ending format | Check whether a file uses Unix or DOS/Windows line endings |
| `:set fileencoding?` | File's character encoding | Check how text is encoded when reading or writing the file |

**Presenter explanation:**  
“These are inspection commands. They do not normally edit our text. They help us understand the editor's configuration and the format of the file.”

### Explain the two file-format commands

- `fileformat` refers to line endings. Common values are `unix` (LF) and `dos` (CRLF).
- `fileencoding` refers to the character encoding used for the file, such as UTF-8.

**Important distinction:** Line-ending format and character encoding are different things.

## Slide 10 — Configuration

Vim can be customized using a configuration file.

- Vim configuration: `~/.vimrc`
- Neovim Lua configuration: `~/.config/nvim/init.lua`
- Neovim Vimscript configuration: `~/.config/nvim/init.vim`

Example Vim settings:

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

**Presenter explanation:**  
“These settings customize the editor. For example, `number` displays line numbers, `tabstop=4` sets the displayed tab width, and `expandtab` inserts spaces instead of tab characters.”

## Slide 11 — Vim and Neovim

**Neovim** is a modern, community-driven fork of Vim. It keeps the modal editing approach and many familiar Vim commands, while offering modern extensibility and Lua-based configuration.

| Vim | Neovim |
|---|---|
| Traditional Vim editor | Modern Vim fork |
| Commonly configured with Vimscript | Supports Vimscript and Lua |
| Widely available on Unix-like systems | Focuses on modern APIs and extensibility |
| Shares the modal editing model | Shares the modal editing model |

**Presenter explanation:**  
“If we learn the main Vim concepts, much of that knowledge also applies to Neovim. Neovim is an alternative for people who want a more modern configuration and extension environment.”

## Slide 12 — Where Vim is useful

Common real-world situations:
- Editing a configuration file on a Linux machine.
- Updating a script on a remote server through SSH.
- Quickly changing text in source code.
- Searching logs or configuration files.
- Making repeated edits using macros and commands.

**Presenter explanation:**  
“One major advantage is that Vim works inside a terminal. When we connect to a remote server, we can edit files without needing a graphical desktop.”

## Slide 13 — Limitations and good practices

**Limitations**
- Modal editing takes time to learn.
- Some advanced features require configuration or plugins.
- Clipboard support depends on the installed build and environment.
- It may not provide every feature of a fully configured graphical IDE by default.

**Good practices**
- Press `Esc` to return to Normal mode when unsure.
- Save important changes regularly with `:w`.
- Use `:help command` to read Vim's built-in documentation.
- Be careful with `:q!`, because it discards unsaved changes.
- Do not delete a swap file until you have checked whether another editing session or recoverable work exists.

## Slide 14 — Short live demonstration

Use this sequence to demonstrate the basic workflow:

```bash
vim demo.txt
```

Inside Vim:

1. Press `i` and type a few lines.
2. Press `Esc` to return to Normal mode.
3. Use `j` and `k` to move.
4. Use `yy` to copy a line.
5. Use `p` to paste it.
6. Use `dd` to delete a line.
7. Use `u` to undo.
8. Type `/word` to search for a word.
9. Type `:wq` to save and quit.

## Slide 15 — Conclusion

**Key points to remember:**

- Vim is a keyboard-driven, modal text editor.
- Normal mode is for navigation and commands; Insert mode is for typing.
- Operators combine with motions and text objects to perform edits.
- Vim supports search, replacement, registers, macros, buffers and split windows.
- Diagnostic commands help inspect the editor and file settings.
- Neovim builds on Vim's editing model with modern extensibility.

**Closing explanation:**  
“Vim may feel different at first because it uses modes and commands. Once we understand the modes and a few basic command patterns, we can edit files efficiently from the terminal.”

---
