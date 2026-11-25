# opencode-plugins

My [OpenCode](https://opencode.ai) setup: the plugins I run, plus my agents, commands and skills.

The plugin sources are a trimmed copy of [rizal72/opencode-plugins](https://github.com/rizal72/opencode-plugins), keeping
the two plugins I actually run. Upstream is MIT; this repository keeps the same license and the original copyright.
The agents and commands are mine, as is the `internet-budget` skill. The `i-have-adhd` skill is vendored from
[ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd), also MIT.

## Plugins

| plugin | what it does | TUI | GUI | npm |
|---|---|---|---|---|
| [`oc-budget`](plugins/oc-budget/README.md) | how much credit is left on the account behind the model: sidebar, footer, `/budget` | sidebar, footer, `/budget` | header widget | `@rizal72/oc-budget` |
| [`oc-session-search`](plugins/oc-session-search/README.md) | `session_search`: keyword search over past session transcripts | none | none | `@rizal72/oc-session-search` |

The other plugins upstream (models-pro, plugin-updates, git, coffee, ponytail-widget, tps-meter, context) are
not copied here.

## Agents

| agent | what it does |
|---|---|
| [`coach`](agents/coach.md) | career coach that runs a CV-to-offer conveyor belt: titles, tailored CVs, interview answers, per-job application packs; expects a project `AGENTS.md` defining the belt and the `interview-speak` skill |
| [`task-runner`](agents/task-runner.md) | works a project's OpenChamber todo (or `Todo.md`) backlog end to end, one experiment at a time, with subagents; reports verdicts at the end and leaves the decision to you |

## Commands

| command | what it does |
|---|---|
| [`bro`](commands/bro.md) | repeat the last response as a tweet |
| [`model-pick`](commands/model-pick.md) | pick the best model for a task, or for continuing the session |
| [`obsidian`](commands/obsidian.md) | read one Obsidian vault file and continue the conversation about it |
| [`prog`](commands/prog.md) | tweet-size summary of progress so far |
| [`sum`](commands/sum.md) | brief overview of the current project |
| [`x`](commands/x.md) | answer in a tweet-sized response |

## Skills

| skill | what it does |
|---|---|
| [`i-have-adhd`](skills/i-have-adhd/SKILL.md) | shape every response for an ADHD reader: action first, numbered steps, state restated each turn, no preamble or closers; stays on until "stop adhd mode" |
| [`internet-budget`](skills/internet-budget/SKILL.md) | check what is already local, estimate the size, and ask before any sizeable download; the connection is metered |

Source of the `internet-budget` skill text: [Articles/Skills/internet-budget.md](https://github.com/Magid-William/Articles/blob/main/Skills/internet-budget.md).
Source of the `i-have-adhd` skill: [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) (MIT).

## Install

### Plugins

Both are published on npm, so they install normally, which also keeps `opencode plugin check/update` working:

```sh
opencode plugin add @rizal72/oc-budget
opencode plugin add @rizal72/oc-session-search
```

`oc-budget` reads the credentials already stored by `opencode auth login` and needs no configuration of its own.

### Agents, commands and skills

Copy the folders into your OpenCode config directory, then restart OpenCode:

```sh
cp -r agents commands skills ~/.config/opencode/
```

On Windows PowerShell:

```powershell
Copy-Item -Recurse -Force agents,commands,skills "$env:USERPROFILE\.config\opencode\"
```

OpenCode discovers agents in `agents/`, commands in `commands/`, and skills in `skills/<name>/SKILL.md`.
Copying overwrites files of the same name, so back up anything you have edited locally first.

## Layout

```
.
├── agents/
│   ├── coach.md
│   └── task-runner.md
├── commands/
│   ├── bro.md
│   ├── model-pick.md
│   ├── obsidian.md
│   ├── prog.md
│   ├── sum.md
│   └── x.md
├── plugins/
│   ├── oc-budget/
│   └── oc-session-search/
├── skills/
│   ├── i-have-adhd/
│   │   ├── agents/
│   │   └── SKILL.md
│   └── internet-budget/
│       └── SKILL.md
├── LICENSE
└── README.md
```

Each directory under `plugins/` is the upstream plugin, unmodified: source, `README.md`, `package.json`.
No build step is needed for the server parts. The GUI parts (`gui.tsx`) ship prebuilt in the npm packages;
a copy loaded by path would need `scripts/build-gui.mjs` from upstream, which is not included here.

## Not in this repo

- `service.json` and the OpenCode auth files: secrets stay local.
- `opencode.jsonc`: machine-specific MCP server paths.
- the `circuitikz` skill: kept local.
- the `interview-speak` skill, the career `AGENTS.md`, and everything under `career/`: they live in the CV project, which `coach` is written for.

## Updating

```sh
git -C C:/Users/MW/opencode-plugins pull     # agents, commands and skills follow the checkout
opencode plugin update                       # the two npm packages
```

Upstream plugins: https://github.com/rizal72/opencode-plugins - issues and fixes for them belong there.
Agents, commands and skills: edit here, then copy them into `~/.config/opencode/` again.
