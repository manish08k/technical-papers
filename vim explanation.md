Vim Cheat Sheet
1. What are Vi and Vim?

Vi is the original text editor for Unix, created in the 1970s. It runs inside the terminal and is controlled entirely from the keyboard.

Vim stands for “Vi Improved”. It is the upgraded version of Vi, with syntax highlighting, multi-level undo, split windows, tabs, macros and plugins. On most modern Linux systems, typing vi actually opens Vim or a light version of it.

In one line: Vim is a fast, keyboard-only text editor that works in the terminal.

2. What is it used for?
Editing source code and scripts
Editing Linux configuration files (such as /etc/hosts or ~/.bashrc)
Working on remote servers over SSH, where no graphical editor exists
Reading and searching log files
Making quick edits without taking your hands off the keyboard
3. The modes of Vim

Vim is a modal editor, which means the keys do different things depending on the current mode. This is the most important idea to understand.

Mode	Purpose	How to enter	How to leave
Normal mode	Move around, delete, copy, paste, run commands. Vim starts here.	Press Esc	Press a key for another mode
Insert mode	Type and add text	i, a, o and others	Esc
Visual mode	Select text	v, V, Ctrl-v	Esc
Command-line mode	Save, quit, search, replace	Press :	Enter or Esc
Replace mode	Overwrite existing text as you type	R	Esc

If you are ever confused, press Esc twice and you will be back in Normal mode.

4. Insert mode commands
Command	Action
i	Insert before the cursor
I	Insert at the start of the line
a	Append after the cursor
A	Append at the end of the line
o	Open a new line below
O	Open a new line above
Esc	Leave Insert mode
5. Visual mode commands

There are three types of Visual mode.

Command	Selects
v	Characters
V	Whole lines
Ctrl-v	A rectangular block (useful for editing columns)

After selecting, use these keys:

Key	Action
y	Copy the selection
d	Delete (cut) the selection
p	Paste
> and <	Indent and un-indent
u and U	Convert to lowercase and UPPERCASE
o	Jump to the other end of the selection

Handy text objects: iw is inside word, i" is inside quotes, i( is inside brackets, ip is paragraph.

6. Moving around
Keys	Action
h j k l	Left, down, up, right
w and b	Next word and previous word
e	End of word
W B E	Same as above, but punctuation counts as part of the word
0	Start of line
^	First non-blank character of the line
$	End of line
gg	First line of the file
G	Last line of the file
42G or :42	Go to line 42
Ctrl-f and Ctrl-b	Full page forward and back
Ctrl-d and Ctrl-u	Half page down and up
H M L	Top, middle and bottom of the screen
Ctrl-o and Ctrl-i	Jump back and forward through your jump history

You can put a number before most movements. For example, 5j moves down 5 lines and 3w jumps 3 words.

7. Editing, deleting, copying and pasting
Command	Action
x	Delete the character under the cursor
r	Replace a single character
dd	Delete (cut) the whole line
3dd	Delete 3 lines
dw	Delete a word
D	Delete to the end of the line
yy	Copy (yank) the whole line
3yy	Copy 3 lines
p	Paste after the cursor or below the line
P	Paste before the cursor or above the line
cw	Change a word
ciw	Change the whole word under the cursor
cc	Change the whole line
C	Change to the end of the line
J	Join the next line to the current one
u	Undo
Ctrl-r	Redo
.	Repeat the last change

Remember the pattern: d is delete, y is copy, c is change, p is paste.

8. The Vim grammar

Vim commands work like short sentences: action + object.

Action	Object	Result
d	w	Delete a word
d	$	Delete to the end of the line
c	iw	Change the word under the cursor
c	i"	Change the text inside quotes
y	ip	Copy a paragraph

Once you know a few actions and a few objects, you can combine them in many ways.

9. Searching and replacing
Command	Action
/word	Search forward
?word	Search backward
n	Next match
N	Previous match
*	Search forward for the word under the cursor
#	Search backward for the word under the cursor
:s/old/new/	Replace the first match on the current line
:s/old/new/g	Replace all matches on the current line
:%s/old/new/g	Replace all matches in the whole file
:%s/old/new/gc	Replace in the whole file, asking for confirmation each time
:10,20s/old/new/g	Replace only between lines 10 and 20
10. Saving and quitting
Command	Action
:w	Save
:q	Quit (only if there are no unsaved changes)
:wq or :x or ZZ	Save and quit
:q! or ZQ	Quit without saving (discards changes)
:w newname	Save a copy under a new name and keep editing the original
:sav newname	Save under a new name and continue editing the new file
:wqa	Save all open files and quit
:w !sudo tee %	Save a file that needs root permission
11. Working with multiple files, splits and tabs
Command	Action
:e file	Open a file
:ls	List open buffers
:bn and :bp	Next and previous buffer
:bd	Close the current buffer
:sp file	Horizontal split
:vs file	Vertical split
Ctrl-w then h j k l	Move between splits
Ctrl-w q	Close the current split
:tabnew	Open a new tab
gt and gT	Next and previous tab

A buffer is the file in memory, a window is a view of a buffer, and a tab is a collection of windows.

12. Marks, macros and registers
Command	Action
ma	Set a mark named a
`a	Jump to mark a
`.	Jump to the last change
qa	Start recording a macro into register a
q	Stop recording
@a	Run the macro
@@	Run the last macro again
50@a	Run the macro 50 times
"+y and "+p	Copy and paste using the system clipboard
13. Useful settings
Command	Action
:set number	Show line numbers
:set nonumber	Hide line numbers
gg=G	Auto-indent the whole file
:help topic	Open the built-in help
:colorscheme name	Change the color theme

A simple starter configuration for ~/.vimrc:

vim
set number
set relativenumber
set tabstop=4 shiftwidth=4 expandtab
set ignorecase smartcase
syntax on
14. Learning order
Survival: vim file, i, Esc, :wq, :q!
Movement: h j k l, w, b, 0, $, gg, G
Editing: dd, yy, p, u, ciw, .
Searching: /word, n, :%s/old/new/gc
Advanced: Visual mode, splits, tabs, macros
15. The top 10 to remember

i, Esc, :wq, :q!, dd, yy, p, u, /word, ciw
