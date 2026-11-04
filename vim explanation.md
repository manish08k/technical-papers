# Vim & Neovim 
> A beginner-to-advanced guide to understanding Vim, explaining how it works, using it efficiently, reviewing its commands, and practising real editing workflows.
>
> This guide complements the **Vim & Neovim Command Cheat Sheet**. The cheat sheet is a command reference; this document explains the concepts behind those commands.

---

# Part 1 — Understand Vim

## 1. What is Vim?

**Vim** stands for **Vi Improved**. It is a powerful, keyboard-driven text editor based on the older Unix editor `vi`.

Vim is commonly used to:
- Edit source code and configuration files.
- Work on remote Linux servers through SSH.
- Edit shell scripts and system configuration.
- Search, replace, and transform large amounts of text.
- Work efficiently without relying on a mouse.

Vim is available on Linux, macOS, and Windows. **Neovim** is a modern, community-driven fork of Vim that keeps much of Vim's editing model while improving extensibility and configuration.

### Vim vs a normal text editor

| Traditional editor | Vim |
|---|---|
| Usually type directly into the document | Switch between editing and command modes |
| Mouse is commonly used | Keyboard-first workflow |
| Actions often use menus and buttons | Actions use short commands and combinations |
| Editing commands may be toolbar-based | Commands can be repeated and combined |
| Automation may require external tools | Macros, registers, and commands are built in |

**Main idea:** Vim is designed around editing text through precise, composable commands.

## 2. Why learn Vim?

1. **Speed:** Navigate and edit without repeatedly reaching for a mouse.
2. **Remote work:** Edit files directly on Linux servers over SSH.
3. **Productivity:** Combine operators and motions to perform edits quickly.
4. **Automation:** Record macros and repeat operations.
5. **Developer workflow:** Edit source code, scripts, logs, and configuration files.
6. **Portability:** The core editing concepts work across many systems.

Vim is not automatically faster for every task. Its benefits come after learning the modes and practising the command patterns.

## 3. What happens when you run `vim file.txt`?

1. The shell starts the Vim executable.
2. Vim opens `file.txt`, or prepares a new buffer if the file does not exist.
3. Vim displays the buffer in a window.
4. You begin in Normal mode.
5. You navigate or issue editing commands.
6. Changes are held in memory until you save.
7. `:w` writes the buffer to disk.
8. `:q` exits Vim when it is safe to do so.

### Important terms

| Term | Meaning |
|---|---|
| Buffer | The in-memory text being edited |
| Window | A viewport that displays a buffer |
| Tab page | A collection of windows |
| Register | A storage location for yanked or deleted text |
| Mark | A saved cursor location |
| Motion | A command that moves the cursor |
| Operator | An action such as delete, change, or yank |
| Text object | A structured text region such as a word or quoted string |
| Mapping | A custom key shortcut |
| Plugin | An extension that adds functionality |

A single buffer can be shown in more than one window. A tab page can contain multiple windows. This is why Vim's tabs are not exactly the same as tabs in many graphical editors.

---

# Part 2 — Vim's Modal Editing Model

## 4. What does modal editing mean?

Vim is a **modal editor**. The keyboard behaves differently depending on the current mode.

For example:
- In Normal mode, `j` moves down.
- In Insert mode, typing `j` inserts the letter `j`.

This is the central concept to understand before learning individual commands.

## 5. The main modes

### Normal mode

This is the default mode. Use it to navigate, delete, copy, paste, search, and run editing commands.

Examples:
- `h`, `j`, `k`, `l` — move.
- `dd` — delete a line.
- `yy` — copy a line.
- `p` — paste.
- `/error` — search for `error`.

### Insert mode

Use Insert mode to type ordinary text.

Enter it with:
- `i` — insert before cursor.
- `a` — append after cursor.
- `o` — open a new line below.
- `O` — open a new line above.
- `I` — insert at the first non-blank character.
- `A` — append at the end of the line.

Press `Esc` to return to Normal mode.

### Visual mode

Use Visual mode to select text.

- `v` — select characters.
- `V` — select whole lines.
- `Ctrl-v` — select a rectangular block.

After selecting, use commands such as `d`, `y`, `c`, `>`, or `<`.

### Command-line mode

Press `:` from Normal mode to enter a command.

Examples:
- `:w` — save.
- `:q` — quit.
- `:set number` — show line numbers.
- `:%s/old/new/g` — replace text throughout the file.

Press `Enter` to run the command and `Esc` to cancel or return.

### Replace mode

Press `R` in Normal mode to overwrite existing characters as you type. Press `Esc` to stop.

## 6. How to avoid getting stuck in Vim

If you are unsure which mode you are in:

1. Press `Esc` two or three times.
2. You should be back in Normal mode.
3. Type `:q!` and press `Enter` to quit without saving, if that is what you intend.

To save and quit, use `:wq`.

**Do not assume `Ctrl-c` is the universal way to leave Vim.** `Esc` is the standard key for returning to Normal mode.

---

# Part 3 — The Vim Command Language

## 7. The most important Vim pattern

Many Vim editing commands follow this structure:

```text
[count] [operator] [motion or text object]
```

Think of it as:

- **Count:** How many times?
- **Operator:** What action?
- **Motion/text object:** Which text?

### Example 1: `dw`

- `d` = delete.
- `w` = move to the beginning of the next word.
- `dw` = delete from the cursor to the next word boundary.

### Example 2: `3dd`

- `3` = three times.
- `dd` = delete a line.
- `3dd` = delete three lines.

### Example 3: `ciw`

- `c` = change (delete selected text and enter Insert mode).
- `iw` = inner word.
- `ciw` = replace the word under the cursor.

### Example 4: `d}`

- `d` = delete.
- `}` = move to the next paragraph boundary.
- `d}` = delete through the next paragraph boundary.

### Common operators

| Operator | Meaning |
|---|---|
| `d` | Delete |
| `c` | Change and enter Insert mode |
| `y` | Yank (copy) |
| `>` | Indent |
| `<` | Unindent |
| `=` | Auto-indent |
| `g~` | Toggle case |
| `gu` | Convert to lowercase |
| `gU` | Convert to uppercase |

### Common motions

| Motion | Meaning |
|---|---|
| `w` | Next word beginning |
| `e` | End of word |
| `b` | Previous word beginning |
| `0` | First column |
| `^` | First non-blank character |
| `$` | End of line |
| `gg` | First line |
| `G` | Last line |
| `}` | Next paragraph |
| `{` | Previous paragraph |
| `%` | Matching bracket |

## 8. Words vs WORDs

Vim distinguishes between a `word` and a `WORD`.

- A **word** is made from letters, digits, and underscores; punctuation separates words.
- A **WORD** is a sequence of non-whitespace characters; whitespace separates WORDs.

Example:

```text
user_name = total-price
```

- `w` treats punctuation such as `=` and `-` as boundaries.
- `W` moves across whitespace-separated chunks.

Use `w`, `e`, and `b` for fine-grained word movement. Use `W`, `E`, and `B` for larger whitespace-separated chunks.

## 9. Motions vs text objects

A motion describes movement from the cursor. A text object identifies a structured region around or under the cursor.

| Text object | Meaning |
|---|---|
| `iw` | Inner word |
| `aw` | A word, including surrounding whitespace |
| `i"` | Inside double quotes |
| `a"` | Double quotes and their contents |
| `i'` | Inside single quotes |
| `a'` | Single quotes and their contents |
| `i(` | Inside parentheses |
| `a(` | Parentheses and their contents |
| `i[` | Inside square brackets |
| `a[` | Square brackets and their contents |
| `i{` | Inside braces |
| `a{` | Braces and their contents |
| `it` | Inside an HTML/XML tag |
| `at` | HTML/XML tag block, including tags |

Examples:
- `diw` — delete the word under the cursor.
- `ci"` — change the text inside double quotes.
- `ya(` — copy the parentheses and their contents.
- `dat` — delete an HTML/XML tag block.

Text objects are particularly useful when editing code.

---

# Part 4 — Essential Editing Skills

## 10. Navigation

### Basic movement

| Key | Action |
|---|---|
| `h` | Left |
| `j` | Down |
| `k` | Up |
| `l` | Right |
| `0` | First column |
| `^` | First non-blank character |
| `$` | End of line |
| `gg` | First line |
| `G` | Last line |
| `25G` | Line 25 |
| `Ctrl-f` | Page down |
| `Ctrl-b` | Page up |
| `Ctrl-d` | Half-page down |
| `Ctrl-u` | Half-page up |
| `zz` | Center current line |

### Word navigation

| Key | Action |
|---|---|
| `w` | Next word |
| `e` | End of word |
| `b` | Previous word |
| `W` | Next WORD |
| `E` | End of WORD |
| `B` | Previous WORD |

### Character search on a line

| Command | Action |
|---|---|
| `fx` | Find next `x` on current line |
| `Fx` | Find previous `x` on current line |
| `tx` | Move just before next `x` |
| `Tx` | Move just after previous `x` |
| `;` | Repeat last character search |
| `,` | Repeat it in the opposite direction |

### Practical navigation example

Given:

```python
def calculate_total(price, quantity):
    return price * quantity
```

- Put the cursor on `calculate_total`.
- Press `0` to go to the first column.
- Press `$` to go to the end of the line.
- Press `w` to move across words.
- Press `%` while on a parenthesis to jump to its matching parenthesis.

## 11. Inserting and changing text

| Command | Action |
|---|---|
| `i` | Insert before cursor |
| `a` | Append after cursor |
| `I` | Insert at first non-blank character |
| `A` | Append at line end |
| `o` | New line below |
| `O` | New line above |
| `s` | Replace one character and enter Insert mode |
| `S` | Replace current line and enter Insert mode |
| `cw` | Change to next word boundary |
| `ciw` | Change inner word |
| `cc` | Change whole line |
| `C` | Change to end of line |
| `r` | Replace one character |
| `R` | Enter Replace mode |

## 12. Deleting text

| Command | Action |
|---|---|
| `x` | Delete character under cursor |
| `X` | Delete character before cursor |
| `dw` | Delete to next word boundary |
| `de` | Delete through end of word |
| `diw` | Delete inner word |
| `daw` | Delete a word and surrounding whitespace |
| `dd` | Delete current line |
| `D` | Delete to end of line |
| `d0` | Delete to first column |
| `d^` | Delete to first non-blank character |
| `dG` | Delete to end of file |
| `dgg` | Delete to beginning of file |
| `3dd` | Delete three lines |

## 13. Undo, redo, and repeat

| Command | Action |
|---|---|
| `u` | Undo last change |
| `Ctrl-r` | Redo |
| `.` | Repeat last change |
| `U` | Undo changes on the current line in traditional Vim behavior |

The dot command is powerful. For example, if you change a word with `ciw`, move to another word, and press `.`, Vim repeats that edit.

## 14. Copy, cut, paste, and registers

Vim uses the term **yank** for copying.

| Command | Action |
|---|---|
| `yy` | Yank current line |
| `3yy` | Yank three lines |
| `yiw` | Yank inner word |
| `y$` | Yank to end of line |
| `p` | Put after cursor / below line |
| `P` | Put before cursor / above line |
| `dd` | Delete (and normally store) current line |
| `:reg` | List registers |
| `"ayy` | Yank line into register `a` |
| `"ap` | Put from register `a` |
| `"_dd` | Delete line without changing normal registers |
| `"+y` | Yank to system clipboard, if supported |
| `"+p` | Put from system clipboard, if supported |

### What is a register?

A register is a named storage location for text.

Important registers:
- `"` — unnamed register.
- `0` — most recent yank.
- `1` through `9` — numbered delete history.
- `a` through `z` — named registers.
- `+` — system clipboard, if supported.
- `_` — black-hole register; discards text.

Example:
1. Type `"ayy` to copy a line into register `a`.
2. Move elsewhere.
3. Type `"ap` to paste from register `a`.

## 15. Visual selection

| Key | Action |
|---|---|
| `v` | Character selection |
| `V` | Line selection |
| `Ctrl-v` | Block selection |
| `gv` | Reselect last visual selection |
| `o` | Move to the other end of selection |
| `d` | Delete selection |
| `y` | Yank selection |
| `c` | Change selection |
| `>` | Indent selection |
| `<` | Unindent selection |
| `=` | Auto-indent selection |
| `U` | Uppercase selection |
| `u` | Lowercase selection |
| `~` | Toggle case |

### Block selection example

To add `// ` to the beginning of several lines:

1. Put the cursor at the first line.
2. Press `Ctrl-v`.
3. Move down to select the lines.
4. Press `I`.
5. Type `// `.
6. Press `Esc`.

This inserts the prefix on each selected line.

---

# Part 5 — Search, Replace, and File Operations

## 16. Searching

| Command | Action |
|---|---|
| `/word` | Search forward |
| `?word` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `*` | Search forward for word under cursor |
| `#` | Search backward for word under cursor |
| `:noh` | Clear current search highlighting |
| `:set hlsearch` | Enable highlighting |
| `:set incsearch` | Show matches while typing |

Useful patterns:
- `/error` — find `error`.
- `/^main` — find `main` at the start of a line.
- `/end$` — find `end` at the end of a line.
- `/error\c` — search without case sensitivity.

## 17. Find and replace

General format:

```vim
:[range]s/old/new/[flags]
```

Examples:

| Command | Action |
|---|---|
| `:s/old/new/` | First match on current line |
| `:s/old/new/g` | All matches on current line |
| `:%s/old/new/g` | All matches in the file |
| `:%s/old/new/gc` | Confirm each replacement |
| `:10,20s/old/new/g` | Lines 10–20 |
| `:.,$s/old/new/g` | Current line through last line |
| `:%s/old/new/gi` | Global replacement, ignore case |
| `:%s/\<cat\>/dog/g` | Replace whole-word `cat` |

### Understand the symbols

- `:` — enter command-line mode.
- `%` — entire file.
- `s` — substitute.
- `old` — search pattern.
- `new` — replacement text.
- `g` — every match on each selected line.
- `c` — ask before each replacement.
- `i` — ignore case.

### Example

Change every occurrence of `python` to `Python`:

```vim
:%s/python/Python/g
```

Ask before each replacement:

```vim
:%s/python/Python/gc
```

## 18. Opening, saving, and closing files

| Command | Action |
|---|---|
| `vim file.txt` | Open a file |
| `:e file.txt` | Open file in current window |
| `:enew` | New empty buffer |
| `:w` | Save |
| `:w new.txt` | Write to another filename |
| `:saveas new.txt` | Save under a new name |
| `:r file.txt` | Insert file contents below cursor |
| `:q` | Quit |
| `:q!` | Quit without saving |
| `:wq` | Save and quit |
| `:x` | Save if changed and quit |
| `ZZ` | Save and quit |
| `ZQ` | Quit without saving |
| `:wa` | Save all buffers |
| `:qa` | Quit all |
| `:qa!` | Quit all without saving |

**Important:** `:q!` discards unsaved changes in the current buffer. Use it only when you really want to discard them.

---

# Part 6 — Buffers, Windows, Tabs, and Navigation History

## 19. Buffers

A buffer is the text Vim has loaded into memory.

| Command | Action |
|---|---|
| `:ls` or `:buffers` | List buffers |
| `:bnext` or `:bn` | Next buffer |
| `:bprevious` or `:bp` | Previous buffer |
| `:bfirst` | First buffer |
| `:blast` | Last buffer |
| `:b3` | Switch to buffer number 3 |
| `:buffer filename` | Switch to a matching buffer |
| `:bd` | Delete current buffer |
| `:wall` | Save all modified buffers |

## 20. Windows and splits

A window is a viewport showing a buffer.

| Command | Action |
|---|---|
| `:split` | Horizontal split |
| `:vsplit` | Vertical split |
| `:split file.txt` | Open file in horizontal split |
| `:vsplit file.txt` | Open file in vertical split |
| `Ctrl-w w` | Move to next window |
| `Ctrl-w h` | Move left |
| `Ctrl-w j` | Move down |
| `Ctrl-w k` | Move up |
| `Ctrl-w l` | Move right |
| `Ctrl-w q` | Close current window |
| `Ctrl-w o` | Keep only current window |
| `Ctrl-w =` | Equalize window sizes |
| `Ctrl-w +` | Increase height |
| `Ctrl-w -` | Decrease height |

## 21. Tabs

A tab page contains one or more windows.

| Command | Action |
|---|---|
| `:tabnew` | New tab |
| `:tabnew file.txt` | Open file in new tab |
| `gt` | Next tab |
| `gT` | Previous tab |
| `2gt` | Go to tab 2 |
| `:tabfirst` | First tab |
| `:tablast` | Last tab |
| `:tabclose` | Close current tab |
| `:tabonly` | Close other tabs |
| `:tabs` | List tab pages |

## 22. Marks and jump history

Marks save positions so you can return to them.

| Command | Action |
|---|---|
| `ma` | Set local mark `a` |
| `'a` | Jump to line of mark `a` |
| `` `a `` | Jump to exact position of mark `a` |
| `mA` | Set global mark `A` |
| `'A` | Jump to global mark `A` |
| `:marks` | List marks |
| `Ctrl-o` | Older jump location |
| `Ctrl-i` | Newer jump location |
| `:jumps` | Show jump list |

---

# Part 7 — Advanced Productivity

## 23. Macros

A macro records keystrokes and allows you to replay them.

Example: record an edit in register `a`.

1. Press `qa` to start recording.
2. Perform the required edit.
3. Press `q` to stop recording.
4. Press `@a` to replay it.
5. Press `10@a` to replay it ten times.
6. Press `@@` to replay the last macro again.

| Command | Action |
|---|---|
| `qa` | Record into register `a` |
| `q` | Stop recording |
| `@a` | Run macro `a` |
| `@@` | Repeat last macro |
| `10@a` | Run macro 10 times |
| `:reg a` | Inspect register `a` |

**Use case:** Apply the same formatting or edit to many similarly structured lines.

## 24. Folds

Folds hide sections of text to make large files easier to read.

| Command | Action |
|---|---|
| `za` | Toggle fold |
| `zo` | Open fold |
| `zc` | Close fold |
| `zR` | Open all folds |
| `zM` | Close all folds |
| `zj` | Next fold |
| `zk` | Previous fold |
| `zf` | Create fold from Visual selection |
| `zd` | Delete fold |
| `:set foldmethod=indent` | Fold based on indentation |
| `:set foldmethod=manual` | Manually define folds |

## 25. Indentation and formatting

| Command | Action |
|---|---|
| `>>` | Indent current line |
| `<<` | Unindent current line |
| `==` | Auto-indent current line |
| `3>>` | Indent three lines |
| `gg=G` | Auto-indent whole file |
| `=%` | Auto-indent around matching bracket |
| `:set tabstop=4` | Display tab width |
| `:set shiftwidth=4` | Indentation width |
| `:set expandtab` | Use spaces instead of tab characters |
| `:set noexpandtab` | Use actual tab characters |
| `:set autoindent` | Keep previous line's indentation |
| `:retab` | Convert tabs/spaces according to settings |

## 26. Running shell commands

| Command | Action |
|---|---|
| `:!ls` | Run `ls` |
| `:!pwd` | Run `pwd` |
| `:!python3 file.py` | Run Python script |
| `:shell` | Open a shell from Vim |
| `:read !date` | Insert command output below cursor |
| `:terminal` | Open an embedded terminal, if supported |
| `Ctrl-z` | Suspend Vim in many Unix terminals |
| `fg` | Resume suspended Vim from the shell |

## 27. Help and built-in documentation

Vim has a comprehensive built-in help system.

| Command | Action |
|---|---|
| `:help` | Open help |
| `:help subject` | Search a topic |
| `:help :w` | Help for save command |
| `:help i_CTRL-r` | Help for Insert-mode key |
| `:help usr_02` | User manual section |
| `:helpgrep keyword` | Search help files |
| `:cnext` | Next help search result |
| `:cprev` | Previous help search result |
| `:version` | Show version and build features |

When unsure about a command, use `:help` rather than guessing.

---

# Part 8 — Configuration and Customization

## 28. Vim and Neovim configuration files

| Editor | Configuration file |
|---|---|
| Vim | `~/.vimrc` |
| Neovim (Lua) | `~/.config/nvim/init.lua` |
| Neovim (Vimscript) | `~/.config/nvim/init.vim` |

Vim commonly uses Vimscript. Neovim supports Lua as a first-class configuration language. Do not paste Lua configuration into `.vimrc`.

## 29. A simple Vim configuration

Add this to `~/.vimrc`:

```vim
" Display
set number
set relativenumber
set cursorline
set showmatch
set signcolumn=yes

" Search
set ignorecase
set smartcase
set incsearch
set hlsearch

" Indentation
set autoindent
set smartindent
set expandtab
set tabstop=4
set shiftwidth=4
set softtabstop=4

" Editing
set mouse=a
set scrolloff=5
set hidden

" Syntax
syntax on
```

### What do these settings do?

| Setting | Explanation |
|---|---|
| `number` | Show absolute line numbers |
| `relativenumber` | Show relative line numbers |
| `cursorline` | Highlight current line |
| `ignorecase` | Search without case sensitivity by default |
| `smartcase` | Use case-sensitive search if pattern has uppercase |
| `incsearch` | Show matches while typing search |
| `hlsearch` | Highlight search matches |
| `expandtab` | Insert spaces when pressing Tab |
| `tabstop=4` | Display a tab as four columns |
| `shiftwidth=4` | Use four columns for indentation |
| `mouse=a` | Enable mouse support |
| `scrolloff=5` | Keep context around the cursor |
| `hidden` | Allow modified buffers to remain hidden |

## 30. Useful settings to know

| Command | Explanation |
|---|---|
| `:set wrap` | Wrap long lines visually |
| `:set nowrap` | Do not wrap long lines |
| `:set list` | Show tabs and trailing spaces |
| `:set spell` | Enable spell checking |
| `:set nospell` | Disable spell checking |
| `:set clipboard=unnamedplus` | Use system clipboard when supported |
| `:set fileformat?` | Show line-ending format |
| `:set fileformat=unix` | Use LF line endings |
| `:set fileformat=dos` | Use CRLF line endings |
| `:set option?` | Display current option value |
| `:set option!` | Toggle a Boolean option |

---

# Part 9 — Vim and Neovim Compared

## 31. What is the difference?

| Area | Vim | Neovim |
|---|---|---|
| Origin | Improved version of Vi | Community fork of Vim |
| Editing model | Modal | Modal |
| Core commands | Vim commands | Mostly compatible with Vim |
| Configuration | Commonly Vimscript | Vimscript and Lua |
| Extensibility | Plugins and scripting | Modern plugin APIs and Lua support |
| Terminal | Available in supported builds | Built-in terminal support |
| Language servers | Usually configured through plugins | Commonly configured through its LSP APIs/plugins |
| Best reason to choose | Traditional, widely available editor | Modern extensibility and Lua-based configuration |

Both are excellent editors. Learn the shared modal editing model first; most core commands transfer between them.

## 32. Install and check the editor

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install vim
sudo apt install neovim
```

### macOS with Homebrew

```bash
brew install vim
brew install neovim
```

### Check versions

```bash
vim --version
nvim --version
which vim
which nvim
```

### Open files

```bash
vim notes.txt
nvim notes.txt
```

On macOS, the built-in Vim may have different features from a Homebrew installation. Check `vim --version` for `+clipboard` or `-clipboard` to understand clipboard support.

---

# Part 10 — Real-World Workflows

## 33. Create and save a file

```bash
vim hello.py
```

Inside Vim:

1. Press `i`.
2. Type:

```python
def greet(name):
    print(f"Hello, {name}!")

greet("World")
```

3. Press `Esc`.
4. Type `:w`.
5. Press `Enter`.
6. Type `:q` and press `Enter`.

Run it from the shell:

```bash
python3 hello.py
```

## 34. Edit a word without deleting the whole line

Suppose the file contains:

```python
user_name = "Manish"
```

To change `user_name`:

1. Move the cursor onto `user_name`.
2. Type `ciw`.
3. Type `name`.
4. Press `Esc`.

Result:

```python
name = "Manish"
```

## 35. Replace a word throughout a file

Suppose `old_name` appears several times.

```vim
:%s/old_name/new_name/gc
```

Vim asks you to confirm each replacement. Press:
- `y` — replace this match.
- `n` — skip this match.
- `a` — replace all remaining matches.
- `q` — stop.

## 36. Comment several lines

For a language using `#` comments:

1. Move to the first line.
2. Press `Ctrl-v`.
3. Select the first character of each target line.
4. Press `I`.
5. Type `# `.
6. Press `Esc`.

For languages using `//`, insert `// ` instead.

The exact comment syntax depends on the programming language.

## 37. Compare and edit two files

```bash
vim file1.py
```

Inside Vim:

```vim
:vsplit file2.py
```

Move between windows with:

```text
Ctrl-w h
Ctrl-w l
```

You can edit both files and save with `:wa`.

For a command-line diff view, Vim also supports:

```bash
vimdiff file1.py file2.py
```

---

# Part 11 — Common Beginner Mistakes

## 38. Mistakes and their fixes

| Mistake | Correct understanding |
|---|---|
| Typing `:w` while in Insert mode | Press `Esc`, then type `:w` |
| Thinking `j` always types the letter j | In Normal mode it moves down; in Insert mode it types `j` |
| Using `:q` with unsaved changes | Save first, or use `:q!` only if discarding changes |
| Confusing `p` and `P` | `p` puts after/below; `P` puts before/above |
| Confusing `yy` and `dd` | `yy` copies; `dd` deletes |
| Confusing `w` and `W` | `w` moves by word; `W` by whitespace-separated WORD |
| Expecting `:s/old/new/` to replace every match | Add `g` for every match on the line |
| Expecting `:s/old/new/g` to affect the whole file | Use `%` as the range |
| Thinking a Vim tab is one file | A tab page can contain multiple windows |
| Assuming clipboard always works | Check build support and clipboard configuration |
| Deleting a swap file immediately | Check for another active session and recover unsaved work first |

## 39. How to recover when Vim shows a swap-file warning

A swap file may indicate:
- The same file is open in another Vim session.
- A previous Vim session crashed.
- A swap file was left behind.

Do not delete it without checking. If another session is editing the file, avoid editing the same file independently. If a previous session crashed, use Vim's recovery option where appropriate:

```bash
vim -r file.txt
```

After recovering, inspect the content and save it. Remove an obsolete swap file only after confirming it is no longer needed.

## 40. Useful recovery and diagnostic commands

| Command | Purpose |
|---|---|
| `:recover` | Recover current file |
| `:preserve` | Preserve current buffer |
| `:swapname` | Show swap file name |
| `:messages` | Show recent messages |
| `:scriptnames` | List loaded scripts |
| `:version` | Show version and features |
| `:set fileformat?` | Check line endings |
| `:set fileencoding?` | Check file encoding |

---

# Part 12 — Explain Vim Clearly (Interview / Review Notes)

## 41. Short explanation: What is Vim?

**Answer:** Vim is a modal, keyboard-driven text editor derived from Vi. It provides separate modes for navigation, editing, selection, and command execution. Its composable commands, text objects, registers, macros, and powerful search-and-replace features make it useful for programming, system administration, and remote server editing.

## 42. What is modal editing?

**Answer:** Modal editing means the editor has different modes for different tasks. In Vim, Normal mode is used for navigation and commands, Insert mode is used to type text, Visual mode is used to select text, and Command-line mode is used to run editor commands.

## 43. What is the difference between Vim and Vi?

**Answer:** Vi is the traditional Unix text editor. Vim means Vi Improved and adds features such as more powerful undo, syntax highlighting, scripting, search capabilities, and other editing improvements. Exact features depend on the installed implementation.

## 44. What is the difference between Vim and Neovim?

**Answer:** Neovim is a community-driven fork of Vim. It maintains the modal editing approach and broad command compatibility while focusing on modern extensibility, APIs, and Lua configuration. Vim remains widely available and is often installed by default on Unix-like systems.

## 45. What is a buffer?

**Answer:** A buffer is the in-memory text associated with a file or editing session. It can exist without being visible in a window. A buffer is written to disk when saved.

## 46. What is a window?

**Answer:** A window is a viewport that displays a buffer. Multiple windows can display the same buffer or different buffers.

## 47. What is a tab page?

**Answer:** A tab page is a collection of windows. It is not necessarily one file per tab, unlike the common tab model in graphical editors.

## 48. What is a register?

**Answer:** A register is a storage location used to hold text that has been yanked, deleted, or otherwise stored. Vim has unnamed, numbered, named, clipboard, and special registers.

## 49. What is a macro?

**Answer:** A macro is a recorded sequence of keystrokes stored in a register. It can be replayed to repeat the same editing operation, which is useful for repetitive text transformations.

## 50. What is the difference between `dd`, `yy`, and `p`?

**Answer:**
- `dd` deletes the current line and stores the deleted text in a register.
- `yy` yanks (copies) the current line.
- `p` puts the stored text after the cursor or below the current line for line-wise text.

## 51. What is the difference between `:w`, `:q`, and `:wq`?

**Answer:**
- `:w` writes (saves) the current buffer.
- `:q` quits if there are no unsaved changes.
- `:wq` saves and quits.

## 52. What is the difference between `d` and `c`?

**Answer:** Both remove text. `d` deletes the selected text and remains in Normal mode. `c` changes the selected text: it deletes it and enters Insert mode so replacement text can be typed.

## 53. What is the difference between `v`, `V`, and `Ctrl-v`?

**Answer:**
- `v` selects characters.
- `V` selects complete lines.
- `Ctrl-v` selects a rectangular block of text.

## 54. Why is Vim useful for Linux administrators?

**Answer:** Vim is often available on Unix-like systems and can edit configuration files directly in a terminal or over SSH. It is useful when a graphical editor is unavailable, and it supports efficient navigation, search, replacement, and editing of system files.

## 55. What are Vim's limitations?

**Answer:** Vim has a learning curve because of its modal model and command combinations. Advanced IDE features may require configuration or plugins. Clipboard integration and some features depend on the installed build. It is not necessary to use Vim for every editing task.

---

# Part 13 — Practice Plan

## 56. Seven-day beginner-to-confident plan

| Day | Topic | Practice goal |
|---|---|---|
| 1 | Modes and saving | Open, edit, save, and quit files |
| 2 | Navigation | Use `h j k l`, `w`, `b`, `0`, `$`, `gg`, `G` |
| 3 | Editing | Practise `dd`, `yy`, `p`, `x`, `ciw`, `u`, `Ctrl-r` |
| 4 | Visual mode | Select characters, lines, and blocks |
| 5 | Search and replace | Search and use `:%s/old/new/gc` |
| 6 | Buffers and windows | Open multiple files and split windows |
| 7 | Macros and review | Record a macro and complete the exercises |

## 57. Hands-on exercises

Use a disposable file:

```bash
vim practice.txt
```

Complete these tasks:

1. Create a file containing at least five lines.
2. Save it and quit.
3. Reopen it and jump to the last line.
4. Return to the first line.
5. Move to the end of a line.
6. Copy a line and paste it below.
7. Delete a line and undo the deletion.
8. Change one word using `ciw`.
9. Search for a word and move between matches.
10. Replace every occurrence of a word in the file.
11. Select three lines in Visual Line mode and indent them.
12. Open a vertical split and switch between the two windows.
13. Record a macro that performs a simple repeatable edit.
14. Save all changes and quit.

## 58. Self-review checklist

Use this to test whether you understand Vim rather than simply memorizing commands.

- [ ] I can explain what a modal editor is.
- [ ] I can switch between Normal and Insert mode.
- [ ] I can save, quit, and discard changes intentionally.
- [ ] I can navigate by characters, words, lines, and pages.
- [ ] I understand operators, motions, and text objects.
- [ ] I can delete, change, yank, and put text.
- [ ] I can use Visual, Visual Line, and Visual Block modes.
- [ ] I can undo, redo, and repeat edits.
- [ ] I can search and replace text safely.
- [ ] I understand buffers, windows, and tab pages.
- [ ] I can use registers and record a macro.
- [ ] I know where Vim and Neovim configuration files are.
- [ ] I can use built-in help.
- [ ] I know how to handle a swap-file warning carefully.

---

# Part 14 — Final Quick Revision

## 59. The 30 commands to learn first

| Goal | Command |
|---|---|
| Return to Normal mode | `Esc` |
| Insert before cursor | `i` |
| Append after cursor | `a` |
| New line below | `o` |
| New line above | `O` |
| Save | `:w` |
| Quit | `:q` |
| Save and quit | `:wq` |
| Quit without saving | `:q!` |
| Move left/down/up/right | `h j k l` |
| Next word | `w` |
| Previous word | `b` |
| End of word | `e` |
| Start of line | `0` |
| First non-blank | `^` |
| End of line | `$` |
| First line | `gg` |
| Last line | `G` |
| Delete line | `dd` |
| Copy line | `yy` |
| Paste | `p` |
| Undo | `u` |
| Redo | `Ctrl-r` |
| Repeat change | `.` |
| Search | `/word` |
| Next match | `n` |
| Select characters | `v` |
| Select lines | `V` |
| Change inner word | `ciw` |
| Replace throughout file | `:%s/old/new/g` |

## 60. The one concept to remember

Do not try to memorize hundreds of commands at once.

Learn this pattern:

```text
[count] + [operator] + [motion or text object]
```

Then practise a small set of commands until they become natural. Vim becomes much easier when you understand how its commands fit together.

---

## Platform notes

- Most core commands work in both Vim and Neovim.
- Some features, such as `:terminal`, clipboard integration, and certain options, depend on the version and build.
- On Linux, use your distribution's package manager. On macOS, Homebrew can install current Vim or Neovim versions.
- `Ctrl` means the Control key. For example, `Ctrl-w` means hold Control and press `w`.
- Always use `:help topic` to verify details for the version installed on your machine.
