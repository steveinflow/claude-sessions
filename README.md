# claude-sessions

A terminal TUI for managing Claude Code sessions. Browse, search, rename, and resume your sessions from a split-view interface powered by tmux.

![Python 3](https://img.shields.io/badge/python-3.8+-blue) ![tmux](https://img.shields.io/badge/requires-tmux-green)

## Features

- **Split view** - Session picker on the left, live Claude terminal on the right
- **Search** - Filter sessions by project name, prompt content, or custom name
- **Rename** - Give sessions memorable names that persist across launches
- **Resume** - Reopen any past session directly from the picker
- **Fullscreen** - Open a session in its own tmux window
- **Toggle picker** - Hide/show the session list with `Ctrl-b p`
- No dependencies beyond Python 3 and tmux

## Requirements

- Python 3.8+
- tmux (`brew install tmux`)
- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code)

## Install

```bash
# Clone
git clone https://github.com/steveinflow/claude-sessions.git

# Add to PATH (pick one)
ln -s "$(pwd)/claude-sessions/claude-sessions" /usr/local/bin/claude-sessions

# Or add an alias
echo "alias cs='~/path/to/claude-sessions/claude-sessions'" >> ~/.zshrc
```

## Usage

```bash
# Launch split-view TUI (default)
claude-sessions

# Picker only, no tmux split
claude-sessions --no-tmux

# Search from command line
claude-sessions -s "deploy"
```

## Keybindings

| Key | Action |
|-----|--------|
| `j/k` or `Up/Down` | Navigate sessions |
| `Enter` | Open session in right pane |
| `o` | Open session in fullscreen tmux window |
| `n` | Start new Claude session |
| `r` | Rename session |
| `v` | View all prompts from a session |
| `c` | View full conversation |
| `R` | Reload session list |
| `/` | Search / filter |
| `g` / `G` | Jump to top / bottom |
| `Tab` | Focus right pane |
| `Ctrl-b p` | Toggle picker visibility |
| `Esc` / `q` | Back / quit |

## How it works

Session data is read from `~/.claude/history.jsonl` and conversation files in `~/.claude/projects/`. Custom session names are stored in `~/.claude/session-names.json`.

The split view uses tmux: the left pane runs the curses picker, and the right pane is a regular shell where `claude --resume <id>` is launched when you select a session.
