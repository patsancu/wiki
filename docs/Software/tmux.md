### [Build tmux from scratch](https://gist.github.com/patsancu/1a169a3a2c306e498ea809e8f30fc5fd)

### Configuration
#### MacOS
set-option -g default-command "reattach-to-user-namespace -l zsh"
#### `~./tmux.conf`

[Config example](https://gist.github.com/komasaru/5574812)

#### [Simple tmux statusline generator ](https://github.com/edkolev/tmuxline.vim)

#### [Generate a fast shell prompt](https://github.com/edkolev/promptline.vim)

### Cheatsheet

https://gist.github.com/patsancu/60bfd4576af7fecd6f8b4329347a108e

### Sessions
```
tmux new -s session_name
```
`^B + d` detach from session without killing anything
`tmux attach -t session_name` attach to sessions

### Plugins

https://github.com/tmux-plugins/tpm
