# Multiplexers

- [Multiplexers](#what-is-a-multiplexer?)
    - [Basic usage](#basic-usage)
    - [Good practices](#good-practices)
- [Screen](#screen)
- [Tmux](#tmux)

---
## What is a Multiplexer?

A multiplexer, like `screen` or `tmux`, is a tool that allows you to manage **multiple terminal sessions** from a single window. 
A multiplexer is like the "tab" feature in a browser. It lets you open multiple "tabs" or sessions within that single terminal window. 
This means you can have one session running a server, another editing a file, and a third watching system logs, all at the same time and all visible from one `screen`.

The most powerful feature of a multiplexer is **persistence**. Once a session is active, you can simply **detach** from the session, leaving it **running in the background**.
Later, when you're ready, you can **re-attach** to that same session and find everything exactly as you left it. It's a lifesaver!

### Basic usage
These tools have a similar workflow, but their keyboard shortcuts are different. 
The key to using them is called the **prefix key**, which you press before the command to tell the multiplexer what you want to do.

This **prefix key** and the various commands can be remapped to the user preferences. Here is a comparison between `screen` and `tmux` of basic commands:

| **Action** | **`tmux` Command** | **`screen` Command** |
|---|---|---|
| Start a new session | `tmux` | `screen` |
| Start a named session | `tmux new -s <my-session>` | `screen -S <my-session>` |
| Default [Prefix] | `Ctrl+b` | `Ctrl+a` |
| Detach from session | `[Prefix] + d` | `[Prefix] + d` |
| List running sessions | `tmux ls` | `screen -ls` |
| Re-attach to a session | `tmux attach -t <my-session>` | `screen -r <my-session>` |
| Create a new window | `[Prefix] + c` | `[Prefix] + c` |
| Switch to next window | `[Prefix] + n` | `[Prefix] + n` |
| Switch to previous window | `[Prefix] + p` | `[Prefix] + p` |

To quit a session from inside just hit `Ctrl+d`.

### Good practices
Multiplexers are persistent and they can become a mess if forgotten, good practices should be followed in order to avoid that!

- **Always use a named session**: It's much easier to **remember and re-attach** to a session named web-server than to one named 12345.pts-0.server.
- **Remember to end sessions**: When you are done with a session remember to end it in order not to leave heavy sessions constantly running in the background. Try at least to check regurarly if you have open sessions left.
- **Know your tool (keymaps/commands)**: Learn the prefix key, and at least how to retrieve the other available commands, these tools are extremely useful! e.g. Renaming windows (`[Prefix]+,` in `tmux`), jump between windows, jump between sessions.


## Screen
[screen](https://www.gnu.org/software/screen/) is older, requires more manual configuration and therefore sometimes results less intuitive. 
As a multiplexer it is able for each session to open several windows in which jump to.

## Tmux
[tmux](https://github.com/tmux/tmux/wiki) is generally considered the more modern and feature-rich. It appears by deafult with a status bar showing your available windows of the current session.
Moreover, it has the ability to generate **split panes** inside the same window.

Here you can find a simple `tmux` [commands cheatsheet](img/tmux-cheat-sheet.png).

Furthermore, the customization is simpler compared to `screen`. Here is an example of a custom config `~/.tmux.conf`:

```shell
# [[ Remap Prefix ]]
unbind C-b                        # Remove previous keymap
set-option -g prefix C-Space      # Set new option as prefix (Ctrl+Space)
bind-key C-Space send-prefix      # Bind new prefix

# [[ Session Configs ]]
set -g detach-on-destroy off      # don't exit from tmux when closing a session
set -g escape-time 0              # zero-out escape time delay
set -g history-limit 1000000      # increase history size (from 2,000)
set -g base-index 1               # start indexing windows at 1 instead of 0
set -g renumber-windows on        # renumber all windows when any window is closed
set -g set-clipboard on           # use system clipboard
set -g mouse on                   # mouse mode on
set-option -g allow-rename off    # stop renaming windows (otherwise tmux continously renames windows)
set -g default-terminal "${TERM}" # terminal created by tmux has the same capabilities and features (like color support) as the terminal you are using to launch it

# [[ Custom Keymaps ]]
bind -n M-h select-pane -L        # use Alt-h without prefix to switch panes
bind -n M-l select-pane -R        # use Alt-l without prefix to swith panes
bind -n M-k select-pane -U        # use Alt-k without prefix to swith panes
bind -n M-j select-pane -D        # use Alt-j without prefix to swith panes
```
