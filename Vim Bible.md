# Vim Bible
[Cheet Sheet](https://vim.rtorr.com/)
---
### Setup
Open config file in vim 
>vim ~/.vimrc

Paste the following config:
```bash
set number
set relativenumber
set ic
set hlsearch

"Replace all is aliased to S"
nnoremap S :%s//g<Left><Left>
```
---
## Key Functions
---
### Useful

| Shortcut | Description                         |
| -------- | ----------------------------------- |
| hjkl     | Move cursor                         |
| ctrl+u   | Page up                             |
| ctrl+d   | Page down                           |
| dd       | Cut line                            |
| dw       | Delete word                         |
| de       | Delete to end of word               |
| db       | Delete to stsrt of word             |
| d$ or D  | Delete until EOL                    |
| d\}      | Delete to end of paragraph          |
| dap      | Delete around paragraph             |
| da)      | Delete around parenthesis           |
| di)      | Deleete inside parenthesis          |
| p        | Paste                               |
| w        | Next word                           |
| b        | Previous word                       |
| \{\}     | Move to next blank line (paragraph) |
| \*       | Move to next instance of word       |
| \#       | Move to previous instance of word   |
| \^       | Beginning of content                |
| 0        | Beginning of line                   |
| \$       | End of line                         |
| o        | Insert mode and new line            |
| O        | Insert mode and new line above      |
| i        | Insert mode                         |
| I        | Insert mode at beginning of line    |
| dt\*     | Delete to *                         |
| v        | Visual select mode                  |
| V        | Select mode by line                 |
| ctrl+q   | Select mode by chunk                |
| \%       | Go to bracket pair                  |
| zz       | Center view to cursor               |
| ZZ       | Save and exit                       |
| ZQ       | Exit without saving                 |
| x        | Cut character                       |
| gg       | Start of file                       |
| G        | End of file                         |
| a        | Append text after word              |
| A        | Append text end of line             |
| c        | Change                              |
| C or c$  | Change line                         |
| da\[     | Delete around (eg: bracket)         |
| ~        | Swap case                           |
| .        | Repeat last command                 |
| r        | Replace single character            |
| R        | Replace multiple                    |
| y        | Yank (copy)                         |
| < or >   | Indent selection                    |
| /        | Search (n for next, N for previous) |
| ?        | Search backwards                    |
| ctrl+g   | Show file location and stats        |
| 500G     | Go to line 500                      |
| ''       | Go back to where you were           |
|          |                                     |

---
### Advanced
| Command       | Description                                 |
| ------------- | ------------------------------------------- |
| :s/old/new/g  | Substitute old for new (sed command)        |
| :%s/\*/txt/g  | Mass substitute / to replace / replace with |
| qd(commands)q | Record macro commands as 'd'                |
| @d            | Executes macro 'd'                          |
| :h (command)  | Help for command                            |
| :earlier 10m  | Go back 10 min                              |
| :later 10m    | Go forward 10 min                           |
| :!            | Run shell command from Vim                  |
| :r FILE_NAME  | Insert file contents                        |
| :r !ls        | Insert ls output in file                    |
| :norm CMD     | Run command CMD in normal mode on selection |

