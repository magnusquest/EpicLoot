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
| V        | Select mode by line                 |
| ctrl+v   | Select mode by chunk                |
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
| C        | Change line                         |
| da\[     | Delete around (eg: bracket)         |
| ~        | Swap case                           |
| .        | Repeat last command                 |
| r        | Replace single character            |
| R        | Replace multiple                    |
| y        | Yank (copy)                         |
| < or >   | Indent selection                    |
| /        | Search                              |
|          |                                     |

---
### Advanced
| Command       | Description                                 |
| ------------- | ------------------------------------------- |
| :%s/\*/txt/g  | Mass substitute / to replace / replace with |
| qd(commands)q | Record macro commands as 'd'                |
| @d            | Executes macro 'd'                          |
| :h (command)  | Help for command                            |
|               |                                             |
