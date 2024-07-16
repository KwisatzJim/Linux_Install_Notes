### VIM commands

yy - Copies a line

yw - Copies a word

y$ - Copies from where your cursor is to the end of a line

v - Highlight one character at a time using arrow buttons or the h, k, j, l buttons

V - Highlights one line, and movement keys can allow you to highlight additional lines

p - Paste whatever has been copied to the unnamed register

d - Deletes highlighted text

dd - Deletes a line of text

dw - Deletes a word

D - Deletes everything from where your cursor is to the end of the line

d0 - Deletes everything from where your cursor is to the beginning of the line

dgg - Deletes everything from where your cursor is to the beginning of the file

d$ – Delete from the current cursor position till the end of the line

dG - Deletes everything from where your cursor is to the end of the file

x - Deletes a single character

u - Undo the last operation; u# allows you to undo multiple actions

Ctrl + r - Redo the last undo

. - Repeats the last action

0 - always moves the cursor to the "first column"

^ - moves the cursor to the first non-blank character of a line

:%s/\[pattern\]/\[replacement\]/g - This replaces all occurrences of a pattern without confirming each one

:%s/\[pattern\]/\[replacement\]/gc - Replaces all occurrences of a pattern and confirms each one

:tabedit file - opens a new tab and will take you to edit "file"

gt - move to the next tab

gT - move to the previous tab

#gt - move to a specific tab number (e.g. 2gt takes you to the second tab)

:tabs - list all open tabs

:tabclose - close a single tab

You can also ‘vi -p file1 file2’ to start off in tab mode with two files

VIM

File management

|  |
|--|

| :e        | reload file                 |
|-----------|-----------------------------|
| :q        | quit                        |
| :q!       | quit without saving changes |
| :w        | write file                  |
| :w {file} | write new file              |
| :x        | write file and exit         |

Navigation

|  |
|--|

| k  | up                                          |
|----|---------------------------------------------|
| h  | left                                        |
| l  | right                                       |
| j  | down                                        |
| w  | next start of word                          |
| W  | next start of whitespace-delimited word     |
| e  | next end of word                            |
| E  | next end of whitespace-delimited word       |
| b  | previous start of word                      |
| B  | previous start of whitespace-delimited word |
| 0  | start of line                               |
| $  | end of line                                 |
| gg | go to first line in file                    |
| G  | go to end of file                           |
| gk | move down one displayed line                |
| gj | move up one displayed line                  |

Insertion

|  |
|--|

| a         | append after the cursor                                  |
|-----------|----------------------------------------------------------|
| A         | append at the end of the line                            |
| i         | insert before the cursor                                 |
| I         | insert at the beginning of the line                      |
| o         | create a new line under the cursor                       |
| O         | create a new line above the cursor                       |
| R         | enter insert mode but replace instead of inserting chars |
| :r {file} | insert from file                                         |

Editing

|  |
|--|

| u          | undo                                 |
|------------|--------------------------------------|
| yy         | yank (copy) a line                   |
| y{motion}  | yank text that {motion} moves over   |
| p          | paste after cursor                   |
| P          | paste before cursor                  |
| <Del> or x | delete a character                   |
| dd         | delete a line                        |
| d{motion}  | delete text that {motion} moves over |

Search and replace

|  |
|--|

| :s/foo/bar/    | replace the first match of 'foo' with 'bar' on the current line only        |
|----------------|-----------------------------------------------------------------------------|
| :s/foo/bar/g   | replace all matches (\`g\` flag) of 'foo' with 'bar' on the current line only |
| :%s/foo/bar/g  | replace all matches of 'foo' with 'bar' in the entire file (\`:%s\`)          |
| :%s/foo/bar/gc | ask to manually confirm (\`c\` flag) each replacement                         |

Multiple windows

|  |
|--|

| :e filename     | edit another file                     |
|-----------------|---------------------------------------|
| :split filename | split window and load another file    |
| ctrl-w up arrow | move cursor up a window               |
| ctrl-w ctrl-w   | move cursor to another window (cycle) |
| ctrl-w\_         | maximize current window               |
| ctrl-w=         | make all equal size                   |
| 10 ctrl-w+      | increase window size by 10 lines      |
| :vsplit file    | vertical split                        |
| :sview file     | same as split, but readonly           |
| :hide           | close current window                  |
| :only           | keep only this window open            |
| :ls             | show current buffers                  |
| :b 2            | open buffer #2 in this windo          |

