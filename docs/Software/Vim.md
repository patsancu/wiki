### Vimrc

* [Vimrc omorante](https://gist.github.com/patsancu/64114dc27543e9b26b7d3180559f5975) or https://github.com/spacepluk/vim-config/blob/master/vimrc
* [Modularize vimrc](https://www.gregjs.com/vim/2016/do-yourself-a-favor-and-modularize-your-vimrc-init-vim/)

### [Regex](http://vimregex.com/)
#### & 
**&** Is replaced with the entire text matched by the search pattern when used in a
replacement string. This is useful when you want to avoid retyping text:
```
:%s/Yazstremski/&, Carl/
```
The replacement will say Yazstremski, Carl. The & can also replace a variable pattern
(as specified by a regular expression). For example, to surround each line from
1 to 10 with parentheses, type:
```
:1,10s/.*/(&)/
```
***
from *Learning the vi and Vim Editors, Seventh Edition by Arnold Robbins, Elbert Hannah, and Linda Lamb*.
#### Insert a space between `#` and the character that follows it
```
:%s/#\(\w\)/# \1/g
```
#### general
```
.  any character except new line
\s whitespace character
\S non-whitespace character
\d digit
\D non-digit
\x hex digit
\X non-hex digit
\o octal digit
\O non-octal digit
\h head of word character (a,b,c...z,A,B,C...Z and _)
\H non-head of word character
\p printable character
\P like \p, but excluding digits
\w word character
\W non-word character
\a alphabetic character
\A non-alphabetic character
\l lowercase character
\L non-lowercase character
\u uppercase character
\U non-uppercase character
```

### Quickfix
`C-w<Enter>` Open file from list

### Vim cool fonts
Linux
```sh
$ mkdir -p ~/.local/share/fonts
$ cd ~/.local/share/fonts && curl -fLo "Droid Sans Mono for Powerline Nerd Font Complete.otf" https://raw.githubusercontent.com/ryanoasis/nerd-fonts/master/patched-fonts/DroidSansMono/complete/Droid%20Sans%20Mono%20for%20Powerline%20Nerd%20Font%20Complete.otf
```
* In vimrc, set
```
set guifont=Droid\ Sans\ Mono\ for\ Powerline\ Plus\ Nerd\ File\ Types\ 11
```

MacOS
```
cd ~/Library/Fonts && curl -fLo "Droid Sans Mono for Powerline Nerd Font Complete.otf" https://raw.githubusercontent.com/ryanoasis/nerd-fonts/master/patched-fonts/DroidSansMono/complete/Droid%20Sans%20Mono%20for%20Powerline%20Nerd%20Font%20Complete.otf
```
* In .vimrc, 
```
set guifont=Droid\ Sans\ Mono\ for\ Powerline\ Plus\ Nerd\ File\ Types:h11
```
* Install [vim-devicons plugin](https://github.com/ryanoasis/vim-devicons), [after](https://github.com/ryanoasis/vim-devicons#set-vimdevicons-to-load-after-these-plugins) NERDTree and others
* Restart terminal
* Change font in terminal

### Make vim automatically read file as some filetype
Insert this line in the file
```
# vim: set filetype=sh
```

## Misc
`:echo expand('%:p')` _print filename with full path_

### Vim diff
#### turn on
:windo diffthis
#### turn off
:windo diffoff
#### move between changes
```[c jump back```
```]c  and forward```

### Movements
* `gg` _Go to beginning of file_
* `G` _Go to end of file_

### Windows et al
* `^w` _Change subwindow_
* `:q` _Command history_

### Search and replace
* +?|& must be escaped for special function
* \r is new line (for replacing)

#### normal mode
* `/wordtosearch` + **Enter** _Search for word_
* `/\cwortosearch` + **Enter**  _Case insensitive search for word_
* `:%s/foo/bar/gci` _Replaces all ocurrences (g) in all the text (%) of the word **foo** by the word **bar**, ignoring cases (i) and asking confirmation (c) for each replacement_
* `:%s/patata//gn` _counts ocurrences of patata in all the text_

### Buffers
* `:ls`
* `:b 2` _go to buffer# 2_
* `:vsp filename` _vertical split_
* `:sp filename` _horizontal split_
* `:bnext` mapped to (Ctrl + → )  _next buffer_
* `:bprev` mapped to (Ctrl + ← ) _previous buffer_
* `:sb` _vertically split buffer on current file_


### External commands and writing (vimtutor# 5)

* `:!command`  _executes an external command._
* `:w FILENAME`  _writes the current Vim file to disk with name FILENAME._
* `v  motion  :w FILENAME`  _saves the Visually selected lines in file FILENAME._
* `:r FILENAME`  _retrieves disk file FILENAME and puts it below the cursor position._
* `:r !dir`  _reads the output of the dir command and puts it below the cursor position._


### Editing 

#### Normal mode
* `:m .+1` _Move line down_
* `:m .-2` _Move line up_
* `cw  _change word (deletes word and switches to insert mode)_
* `ci"` _change insde " (also, ([{, etc)_
* 55,60d _deleted lines 55-60 (can be applied to other actions)_
* `gg=G` _format all file_
* `# ngg` _go to line number # n_
* `:set list` _show whitespaces_
* `u` _undo_
* `U` _undo changes on line_
* `CTRL + R` _redo_
* `A` _goes to end of line and enters insert mode_
* `*` _goes to next appearance of the word pointed by the cursor_

* `zb` _goes to bottom of screen_
* `zz` _goes to middle of screen_
* `zt` _goes to top of screen_
#### Screen moving
* `^f` _move one screen forward_
* `^b` _move one screen backwards_



#### Insert mode
* `ctrl+Space` (was `Ctrl+N`) _Autocomplete_

### Visual Mode
* `v` _visual mode_
* `V` _visual line mode_
* `CTRL + v` _visual block mode_

##### Add text to multiple lines (at the same cursor position: column)
* Enter visual block mode
* Select lines
* Type `I` (capital i)
* Write text
* Press `Escape`

## Plugins

**NERDTree**

_From within NERDTree Window_

* `m` _bring up the NERDTree Filesystem Menu_
   * `a` create new file
* `t` _open in tab_
* `i` _open in h split_
* `s` _open in v split_
* `O` expand selected folder recursively_
* `I` _show/hide hidden files_
* `C` _change root to highlighted folder_

**[Gist](https://github.com/mattn/gist-vim)**

* `:'<,'>Gist` Post selected text to gist

