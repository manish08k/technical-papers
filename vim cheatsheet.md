
## 1. Start Vim

| Command | Purpose |
|---|---|
| `vim` | Open Vim |
| `vim file.txt` | Open or create a file |
| `vim file1 file2` | Open multiple files |
| `vim + file.txt` | Open file at the end |
| `vim +10 file.txt` | Open file at line 10 |
| `vim +/word file.txt` | Open file at first match of `word` |
| `vim -R file.txt` | Open file read-only |
| `view file.txt` | Open in read-only mode |
| `nvim file.txt` | Open with Neovim |

## 2. Vim modes

| Mode | How to enter | What it does |
|---|---|---|
| Normal | `Esc` | Navigate, delete, copy, paste, and run commands |
| Insert | `i`, `a`, `o`, etc. | Type text |
| Visual | `v` | Select characters |
| Visual Line | `V` | Select complete lines |
| Visual Block | `Ctrl-v` | Select a rectangular block |
| Command-line | `:` | Run commands such as save, quit, and substitute |
| Replace | `R` | Overwrite existing text |
| Select | `gh` / `gH` | Select text using Select mode |

**Remember:** `Esc` returns to Normal mode from most other modes.

## 3. Save and quit

Run these from Normal mode:

| Command | Purpose |
|---|---|
| `:w` | Save |
| `:w file.txt` | Save as another filename |
| `:saveas file.txt` | Save under a new name |
| `:w!` | Force save when permitted |
| `:q` | Quit |
| `:q!` | Quit without saving changes |
| `:wq` | Save and quit |
| `:x` | Save and quit if changed |
| `ZZ` | Save and quit |
| `ZQ` | Quit without saving |
| `:wa` | Save all open buffers |
| `:qa` | Quit all windows |
| `:qa!` | Quit all without saving |
| `:wqa` | Save all and quit |

## 4. Moving the cursor

### Basic movement

| Key | Movement |
|---|---|
| `h` | Left |
| `j` | Down |
| `k` | Up |
| `l` | Right |
| `0` | First column |
| `^` | First non-blank character |
| `$` | End of line |
| `g_` | Last non-blank character |
| `gg` | First line of file |
| `G` | Last line of file |
| `:25` | Go to line 25 |
| `25G` | Go to line 25 |
| `25gg` | Go to line 25 |
| `Ctrl-f` | Page down |
| `Ctrl-b` | Page up |
| `Ctrl-d` | Half-page down |
| `Ctrl-u` | Half-page up |
| `zz` | Center current line |
| `zt` | Put current line at top |
| `zb` | Put current line at bottom |

### Word movement

| Key | Movement |
|---|---|
| `w` | Beginning of next word |
| `W` | Beginning of next WORD (whitespace-separated) |
| `e` | End of word |
| `E` | End of WORD |
| `b` | Beginning of previous word |
| `B` | Beginning of previous WORD |
| `ge` | End of previous word |
| `f{char}` | Move to next occurrence of character on line |
| `F{char}` | Move backward to character on line |
| `t{char}` | Move just before next character |
| `T{char}` | Move just after previous character |
| `;` | Repeat last `f`, `F`, `t`, or `T` in same direction |
| `,` | Repeat it in the opposite direction |

### Screen and matching movement

| Key | Purpose |
|---|---|
| `H` | Top visible line |
| `M` | Middle visible line |
| `L` | Bottom visible line |
| `%` | Jump between matching brackets/parentheses |
| `{` / `}` | Previous / next paragraph |
| `(`/`)` | Previous / next sentence |
| `Ctrl-o` | Jump to older location |
| `Ctrl-i` | Jump to newer location |
| `gd` | Go to local declaration of word under cursor |
| `gD` | Go to global declaration of word under cursor |

## 5. Insert and append text

| Key | Purpose |
|---|---|
| `i` | Insert before cursor |
| `I` | Insert at first non-blank character |
| `a` | Append after cursor |
| `A` | Append at end of line |
| `o` | Open new line below |
| `O` | Open new line above |
| `s` | Delete character and enter Insert mode |
| `S` | Replace current line and enter Insert mode |
| `gi` | Resume Insert mode at previous insertion position |
| `Esc` | Return to Normal mode |

## 6. Delete, change, and replace

Vim uses operators with motions. For example, `d` means delete and `w` means move to the next word.

| Command | Purpose |
|---|---|
| `x` | Delete character under cursor |
| `X` | Delete character before cursor |
| `dw` | Delete from cursor to next word start |
| `de` | Delete through end of word |
| `diw` | Delete inner word |
| `daw` | Delete a word including surrounding whitespace |
| `dd` | Delete current line |
| `D` or `d$` | Delete to end of line |
| `d0` | Delete to beginning of line |
| `d^` | Delete to first non-blank character |
| `dG` | Delete from current line to end of file |
| `dgg` | Delete from current line to beginning of file |
| `3dd` | Delete 3 lines |
| `cw` | Change from cursor to next word boundary |
| `ciw` | Change inner word |
| `caw` | Change a word including surrounding whitespace |
| `cc` | Change entire line |
| `C` or `c$` | Change to end of line |
| `r<char>` | Replace one character |
| `R` | Enter Replace mode |
| `J` | Join current line with next line |
| `gJ` | Join lines without adding a space |
| `u` | Undo |
| `Ctrl-r` | Redo |
| `.` | Repeat the last change |

**Text objects:** `iw` = inner word, `aw` = a word plus whitespace, `i"` = inside quotes, `a"` = quotes and contents, `i(` = inside parentheses, `a(` = parentheses and contents, `it` = inside an HTML/XML tag.

Examples:
- `ci"` changes text inside quotes.
- `da(` deletes parentheses and their contents.
- `yiw` copies the word under the cursor.

## 7. Copy, cut, and paste

Vim calls copying **yanking**.

| Command | Purpose |
|---|---|
| `yy` or `Y` | Copy current line |
| `3yy` | Copy 3 lines |
| `yw` | Copy to next word boundary |
| `yiw` | Copy inner word |
| `y$` | Copy to end of line |
| `y0` | Copy to beginning of line |
| `p` | Paste after cursor / below line |
| `P` | Paste before cursor / above line |
| `dd` | Cut current line |
| `dw` | Cut text to next word boundary |
| `"+y` | Copy to system clipboard (if clipboard support is available) |
| `"+p` | Paste from system clipboard |
| `:reg` | Show registers |

### Registers

| Command | Purpose |
|---|---|
| `:reg` | Display registers |
| `"ayy` | Copy line into register `a` |
| `"ap` | Paste from register `a` |
| `"add` | Delete line into register `a` |
| `"_dd` | Delete line without overwriting normal registers |
| `"+y` | Yank to system clipboard |
| `"+p` | Paste from system clipboard |
| `"0p` | Paste the most recent yank |

Clipboard support depends on how Vim/Neovim was built and configured. Check Vim with `:version` and look for `+clipboard`.

## 8. Visual selection

| Key | Purpose |
|---|---|
| `v` | Start character-wise selection |
| `V` | Start line-wise selection |
| `Ctrl-v` | Start block-wise selection |
| `gv` | Reselect previous visual selection |
| `o` | Move cursor to other end of selection |
| `d` | Delete selection |
| `y` | Copy selection |
| `c` | Change selection |
| `>` | Indent selection |
| `<` | Unindent selection |
| `=` | Auto-indent selection |
| `u` | Make selected text lowercase |
| `U` | Make selected text uppercase |
| `~` | Toggle case |

## 9. Indentation and formatting

| Command | Purpose |
|---|---|
| `>>` | Indent current line |
| `<<` | Unindent current line |
| `==` | Auto-indent current line |
| `3>>` | Indent 3 lines |
| `gg=G` | Auto-indent the whole file |
| `=%` | Auto-indent around matching bracket |
| `:set number` | Show line numbers |
| `:set nonumber` | Hide line numbers |
| `:set relativenumber` | Show relative line numbers |
| `:set norelativenumber` | Hide relative line numbers |
| `:set tabstop=4` | Set displayed tab width |
| `:set shiftwidth=4` | Set indentation width |
| `:set expandtab` | Convert typed tabs to spaces |
| `:set noexpandtab` | Use actual tab characters |
| `:set autoindent` | Copy indentation from previous line |
| `:set smartindent` | Enable smart indentation |
| `:retab` | Convert tabs/spaces according to settings |

## 10. Search

| Command | Purpose |
|---|---|
| `/word` | Search forward |
| `?word` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `*` | Search forward for word under cursor |
| `#` | Search backward for word under cursor |
| `g*` | Search forward for partial word |
| `g#` | Search backward for partial word |
| `:set hlsearch` | Highlight matches |
| `:set nohlsearch` | Disable search highlighting |
| `:set incsearch` | Show matches while typing |
| `:nohlsearch` or `:noh` | Clear current search highlighting |
| `\c` in a pattern | Ignore case for that search |
| `\C` in a pattern | Match case for that search |

Examples:
- `/error` — search for `error`.
- `/error\c` — case-insensitive search.
- `/^main` — find lines beginning with `main`.
- `/end$` — find lines ending with `end`.

## 11. Find and replace

General format:

```vim
:[range]s/old/new/[flags]
```

| Command | Purpose |
|---|---|
| `:s/old/new/` | Replace first match on current line |
| `:s/old/new/g` | Replace all matches on current line |
| `:%s/old/new/g` | Replace all matches in entire file |
| `:%s/old/new/gc` | Confirm each replacement |
| `:10,20s/old/new/g` | Replace in lines 10–20 |
| `:.,$s/old/new/g` | Replace from current line to end |
| `:%s/old/new/gi` | Replace all, ignoring case |
| `:%s/\<cat\>/dog/g` | Replace whole-word `cat` with `dog` |
| `:s/^/# /` | Add `# ` at start of current line |
| `:%s/^/# /` | Add `# ` at start of every line |
| `:%s/\s\+$//e` | Remove trailing whitespace |

Common flags:
- `g` — all matches on each line.
- `c` — ask for confirmation.
- `i` — ignore case.
- `I` — match case.
- `n` — report number of matches without replacing.
- `e` — suppress error when no match is found.

## 12. Files, buffers, and navigation

A **buffer** is a file loaded into Vim. A buffer can exist without being visible in a window.

| Command | Purpose |
|---|---|
| `:e file.txt` | Open file |
| `:enew` | Create an empty buffer |
| `:w` | Save current buffer |
| `:saveas new.txt` | Save buffer under another name |
| `:r file.txt` | Insert another file's contents below cursor |
| `:r !date` | Insert output of shell command |
| `:files` or `:ls` | List buffers |
| `:bnext` or `:bn` | Next buffer |
| `:bprevious` or `:bp` | Previous buffer |
| `:bfirst` | First buffer |
| `:blast` | Last buffer |
| `:b3` | Switch to buffer number 3 |
| `:buffer filename` | Switch to matching buffer |
| `:bdelete` or `:bd` | Delete current buffer |
| `:wall` | Save all modified buffers |
| `:edit!` | Reload current file and discard unsaved changes |

## 13. Windows and splits

| Command | Purpose |
|---|---|
| `:split` or `:sp` | Horizontal split |
| `:split file.txt` | Open file in horizontal split |
| `:vsplit` or `:vs` | Vertical split |
| `:vsplit file.txt` | Open file in vertical split |
| `Ctrl-w w` | Move to next window |
| `Ctrl-w h` | Move to left window |
| `Ctrl-w j` | Move to window below |
| `Ctrl-w k` | Move to window above |
| `Ctrl-w l` | Move to right window |
| `Ctrl-w q` | Close current window |
| `Ctrl-w o` | Keep only current window |
| `Ctrl-w =` | Make windows equal size |
| `Ctrl-w +` | Increase window height |
| `Ctrl-w -` | Decrease window height |
| `Ctrl-w >` | Increase window width |
| `Ctrl-w <` | Decrease window width |
| `:only` | Close all other windows |

## 14. Tabs

Vim tabs are collections of windows, not simply file tabs.

| Command | Purpose |
|---|---|
| `:tabnew` | Open a new tab |
| `:tabnew file.txt` | Open file in a new tab |
| `:tabnext` or `gt` | Next tab |
| `:tabprevious` or `gT` | Previous tab |
| `:tabfirst` | First tab |
| `:tablast` | Last tab |
| `:tabclose` | Close current tab |
| `:tabonly` | Close all other tabs |
| `:tabs` | List tabs |
| `2gt` | Go to tab 2 |

## 15. Marks and jump list

Marks let you save locations and jump back to them.

| Command | Purpose |
|---|---|
| `ma` | Set local mark `a` |
| `'a` | Jump to line of mark `a` |
| `` `a `` | Jump to exact position of mark `a` |
| `mA` | Set global mark `A` |
| `'A` | Jump to global mark `A` |
| `:marks` | List marks |
| `''` | Jump to previous context line |
| `` `` `` | Jump to previous exact position |
| `:jumps` | Show jump list |
| `Ctrl-o` | Older jump |
| `Ctrl-i` | Newer jump |

## 16. Macros and repeat actions

Macros record keystrokes and replay them.

| Command | Purpose |
|---|---|
| `qa` | Start recording into register `a` |
| `q` | Stop recording |
| `@a` | Run macro in register `a` |
| `@@` | Repeat last executed macro |
| `10@a` | Run macro 10 times |
| `qA` | Append recording to register `a` |
| `:reg a` | Inspect register `a` |

Example workflow:
1. Move to a line and type `qa`.
2. Perform the edits you want to repeat.
3. Press `q` to stop recording.
4. Move to another line and run `@a`.
5. Use `10@a` to repeat it ten times.

## 17. Folds

Folds hide sections of text so you can focus on other parts.

| Command | Purpose |
|---|---|
| `za` | Toggle fold under cursor |
| `zo` | Open fold |
| `zc` | Close fold |
| `zR` | Open all folds |
| `zM` | Close all folds |
| `zj` | Move to next fold |
| `zk` | Move to previous fold |
| `zf` | Create fold from selected text (Visual mode) |
| `zd` | Delete fold under cursor |
| `:set foldmethod=indent` | Fold based on indentation |
| `:set foldmethod=manual` | Use manually created folds |

## 18. Useful command-line and shell commands

| Command | Purpose |
|---|---|
| `:!ls` | Run shell command without leaving Vim |
| `:!pwd` | Run `pwd` |
| `:!python3 file.py` | Run Python script |
| `:shell` | Open a shell; type `exit` to return |
| `Ctrl-z` | Suspend Vim in many Unix terminals |
| `fg` | Resume suspended Vim in the shell |
| `:read !date` | Insert command output below cursor |
| `:write !command` | Send buffer to a shell command |
| `:terminal` | Open terminal inside Vim (if supported) |
| `:term` | Short form of `:terminal` |

## 19. Help system

| Command | Purpose |
|---|---|
| `:help` | Open Vim help |
| `:help subject` | Search help for a topic |
| `:help :w` | Help for the save command |
| `:help i_CTRL-r` | Help for a key in Insert mode |
| `:help usr_02` | Open a section of the user manual |
| `:helpgrep keyword` | Search help files |
| `:cnext` | Next help search result |
| `:cprev` | Previous help search result |
| `:q` | Close help window |

## 20. Useful settings

Use `:set` for temporary settings. Put preferred settings in `~/.vimrc` (Vim) or `~/.config/nvim/init.lua` (Neovim).

| Command | Purpose |
|---|---|
| `:set number` | Show absolute line numbers |
| `:set relativenumber` | Show relative line numbers |
| `:set cursorline` | Highlight current line |
| `:set showmatch` | Briefly highlight matching bracket |
| `:set ignorecase` | Case-insensitive search |
| `:set smartcase` | Use case-sensitive search when pattern has uppercase |
| `:set wrap` | Wrap long lines visually |
| `:set nowrap` | Do not wrap long lines |
| `:set mouse=a` | Enable mouse in all modes |
| `:set clipboard=unnamedplus` | Use system clipboard when supported |
| `:set scrolloff=5` | Keep 5 screen lines around cursor |
| `:set signcolumn=yes` | Always show sign column |
| `:set list` | Show tabs and trailing spaces |
| `:set listchars=tab:>-,trail:·,extends:>,precedes:<` | Customize invisible-character display |
| `:set spell` | Enable spell checking |
| `:set nospell` | Disable spell checking |
| `:syntax on` | Enable syntax highlighting |
| `:colorscheme desert` | Set a colorscheme (if installed) |
| `:set` | Display changed options |
| `:set option?` | Display current value of an option |

### Example `~/.vimrc`

```vim
" Basic settings
set number
set relativenumber
set cursorline
set showmatch
set ignorecase
set smartcase
set incsearch
set hlsearch
set autoindent
set smartindent
set expandtab
set tabstop=4
set shiftwidth=4
set softtabstop=4
set mouse=a
set scrolloff=5
syntax on
```

## 21. Recovery and troubleshooting

| Command / action | Purpose |
|---|---|
| `vim -r file.txt` | Recover a file from a swap file |
| `:recover` | Recover current file |
| `:preserve` | Preserve current buffer to swap file |
| `:swapname` | Show swap file name |
| `:set fileformat?` | Check line-ending format |
| `:set fileformat=unix` | Use Unix LF line endings |
| `:set fileformat=dos` | Use Windows CRLF line endings |
| `:set encoding?` | Check internal encoding |
| `:set fileencoding?` | Check file encoding |
| `:messages` | Show recent messages |
| `:scriptnames` | List sourced Vim scripts |
| `:version` | Show Vim version and build features |

**Swap file warning:** If Vim reports an existing swap file, do not automatically delete it. Another Vim session may still be editing the file. Check whether the other session is active and recover unsaved work when appropriate.

## 22. Vim vs Neovim configuration locations

| Editor | Main configuration |
|---|---|
| Vim | `~/.vimrc` |
| Vim config directory | `~/.vim/` |
| Neovim | `~/.config/nvim/init.lua` |
| Neovim Vimscript config | `~/.config/nvim/init.vim` |
| Vim data directory | `~/.vim/` |
| Neovim data directory | `~/.local/share/nvim/` |

Neovim supports Lua configuration. Vim commonly uses Vimscript in `~/.vimrc`. Do not paste Lua configuration into `.vimrc`.

## 23. Essential Vim command patterns

Many Vim commands follow this structure:

```text
[count] [operator] [motion]
```

Examples:

| Pattern | Meaning |
|---|---|
| `d` + `w` = `dw` | Delete to next word boundary |
| `c` + `i` + `w` = `ciw` | Change inner word |
| `y` + `$` = `y$` | Yank to end of line |
| `3` + `dd` = `3dd` | Delete 3 lines |
| `2` + `w` = `2w` | Move forward 2 words |
| `d` + `}` = `d}` | Delete to next paragraph boundary |
| `g` + `g` = `gg` | Go to first line |

Useful operators:
- `d` — delete
- `c` — change (delete and enter Insert mode)
- `y` — yank (copy)
- `>` — indent
- `<` — unindent
- `=` — auto-indent
- `g~` — toggle case
- `gu` — lowercase
- `gU` — uppercase

Useful motions:
- `w`, `e`, `b` — word movement
- `0`, `^`, `$` — line positions
- `gg`, `G` — file positions
- `}`, `{` — paragraph movement
- `%` — matching bracket

## 24. Beginner practice routine

Try these in a disposable file:

1. `vim practice.txt` — open a practice file.
2. Press `i` and type 3–5 lines.
3. Press `Esc`, then `:w` to save.
4. Use `gg`, `G`, `0`, and `$` to
