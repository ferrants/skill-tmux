# skill-tmux

A [Claude Code plugin](https://code.claude.com/docs/en/plugins) that teaches Claude how to remote-control tmux sessions — sending keystrokes, capturing pane output, and driving interactive CLIs like `python`, `gdb`, `node`, etc.

## Install

```sh
npx skills add ferrants/skill-tmux
```

Or for a specific project only:

```sh
npx skills add ferrants/skill-tmux --scope project
```

### Customize it

Clone the repo and ask your AI coding tool to tailor the skill to your specific workflows:

```sh
git clone https://github.com/ferrants/skill-tmux.git
```

## What it does

Once installed, Claude gains the `/tmux` skill and can automatically:

- **Target panes and windows** — address any `{session}:{window}.{pane}`
- **Send input safely** — literal sends, control keys (`C-c`, `C-d`, `Escape`), and properly quoted commands
- **Capture output** — scrape pane history for inspection and pattern matching

This is useful when you need Claude to interact with long-running processes, REPLs, debuggers, or anything that requires a persistent terminal session.

## Usage

Invoke the skill directly:

```
/tmux
```

Or Claude will invoke it automatically when the task involves interactive terminal work.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- `tmux` installed and available on your PATH

## License

MIT
