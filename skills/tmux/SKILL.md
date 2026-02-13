---
name: tmux
description: "Remote control tmux sessions for interactive CLIs (python, gdb, etc.) by sending keystrokes and scraping pane output."
---

# tmux Skill

Use tmux as a programmable terminal multiplexer for interactive work.

## Targeting panes and windows

- Target format: `{session}:{window}.{pane}`, defaults to `:0.0` if omitted.
- Inspect sessions: `tmux list-sessions`. Do this if it's not clear which session to use.
- Inspect windows: `tmux list-windows -t {session_name}`. Do this if it's not clear which window to use in a session.

## Sending input safely

- Prefer literal sends to avoid shell splitting: `tmux send-keys -t {target} -l -- "$cmd"`
- When composing inline commands, use single quotes or ANSI C quoting to avoid expansion: `tmux ... send-keys -t {target} -- $'python3 -m http.server 8000'`.
- To send control keys: `tmux ... send-keys -t {target} C-c`, `C-d`, `C-z`, `Escape`, etc.
- For example, to grab the logs on the third screen of the 'map' session, you'd run `tmux send-keys -t map:2 'ls -laht' C-m`.

## Watching output

- Capture recent 200 lines of history (joined lines to avoid wrapping artifacts): `tmux capture-pane -p -J -t {target} -S -200`.
- When giving instructions to a user, **explicitly print a copy/paste monitor command** alongside the action don't assume they remembered the command.

- `-t`/`--target` pane target (required)
- `-p`/`--pattern` regex to match (required); add `-F` for fixed string
- `-T` timeout seconds (integer, default 15)
- `-i` poll interval seconds (default 0.5)
- `-l` history lines to search from the pane (integer, default 1000)
- Exits 0 on first match, 1 on timeout. On failure prints the last captured text to stderr to aid debugging.
