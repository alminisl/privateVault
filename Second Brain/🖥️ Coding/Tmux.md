
https://gist.github.com/michaellihs/b6d46fa460fa5e429ea7ee5ff8794b96

Shortcuts
=========

| Key(s)  | Description |
| :-----: | ----------- |
| `CTRL`+`b` `<command>` | sends `<command>` to tmux instead of sending it to the shell |
| | **General Commands** |
| `?` | shows a list of all commands (`q`closes the list) |
| `:` | enter a tmux command |
| | **Working with Windows** |
| `c` | creates a new window |
| `,` | rename current window |
| `p` | switch to previous window |
| `n` | switch to next window |
| `w` | list windows (and then select with arrow keys) |
| | **Working with Panes** |
| `%`          | split window vertically |
| `"`          | split window horizontally <br> requires `bind - split-window -v` in our `.tmux.conf` |
| →          | go to right pane |
| ←          | go to left pane |
| ↑          | go to upper pane |
| ↓          | go to lower pane |
| | **Working with Sessions** |
| `d` | detach from session |




## Session management 

`tmux new -s <name>`
`tmux detach`
`tmux ls`
`tmux attach -t <name>`

``
`ctrl` + `a` + `s` - View Sessions in tmux 


### More information can be found in this video 

https://www.youtube.com/watch?v=U-omALWIBos
