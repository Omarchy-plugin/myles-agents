# myles.agents

A ranked fleet of every coding agent installed on the machine, with token totals, daily trends, and one-click launch.

> **Derived work.** Forked from Omarchy's built-in `omarchy.agents` and substantially modified.
> See [Credits](#credits) for licensing.

A ranked fleet of every coding agent installed on the machine, with token totals, daily
trends, and one-click launch.

## What it does

- **Auto-discovers** installed agent CLIs (Claude, Codex, OpenCode, Pi, Crush, Cursor CLI,
  OpenClaw, Copilot, Fireworks, Grok, Hermes, Muse, OMP, and others) — no manual config.
- **Ranks** agents by token usage, with per-agent cost rates you can set.
- **Trends:** daily and all-time token totals, plus a copyable usage summary.
- **Launch:** right-click any agent to start it.
- **Synced aggregation:** optionally write this machine's local usage snapshot to a folder
  synced by Syncthing/Dropbox/rsync and merge snapshots from your other machines.

## Configuration

All settings live in the widget's own settings sheet:

| Setting | Meaning |
| --- | --- |
| `costRates` | Per-model USD per 1M tokens, as JSON, e.g. `{"model":{"input":5,"output":20}}` |
| `refreshIntervalSec` | Usage refresh interval, 30–3600s |
| `syncMode` | `Off` or `On` — multi-machine aggregation |
| `syncDir` | Folder synced by Syncthing, Dropbox, rsync, … |
| `syncFileName` | Defaults to `<hostname>.json`; use a different name per machine |
| `syncDeviceId` | Stable display name used in the synced aggregate |

Token sources can overlap between providers, so per-provider totals are an **upper bound**,
not an exact sum.

## Requirements

- `omarchy-agent-usage` (ships with Omarchy) supplies the usage data.
- Optional: `omarchy-agent` and the launch helpers. Providers you have not installed simply
  do not appear.
- `launch-agent.sh` starts a detected agent's TUI.

## Network calls

None. Usage is read from local agent session files.

## Install

```bash
omarchy plugin add https://github.com/Omarchy-plugin/myles-agents.git --enable --yes
```

That clones, validates, installs to `~/.config/omarchy/plugins/myles.agents/`, and places it on your bar.

The stock `omarchy.agents` widget does the same job and will fight with this one. Turn it off:

```bash
omarchy plugin disable omarchy.agents
```

## Update

```bash
omarchy plugin update myles.agents --yes
```

Or update every git-managed plugin at once:

```bash
omarchy plugin update --yes
```

## Uninstall

omarchy plugin enable omarchy.agents   # if you want the built-in back

omarchy plugin remove myles.agents --yes

## Credits

- Omarchy — <https://omarchy.org> — MIT, © David Heinemeier Hansson. `omarchy.agents` is the base this is forked from.
- Mylesoft — <https://github.com/Omarchy-plugin> — modifications.

Plugins run unsandboxed inside the long-lived `omarchy-shell` process with your user
permissions. Review the source before enabling anything you did not write.
