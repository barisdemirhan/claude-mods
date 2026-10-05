# claude-mods

Mods for [Claude Code](https://claude.com/claude-code) by Barış Demirhan, in one marketplace. A mod is a plugin that draws inside Claude Code itself: a pane, a band above the prompt, a label on the hint line.

## Install

Add the marketplace once, then install the mods you want:

```sh
claude plugin marketplace add barisdemirhan/claude-mods
claude plugin install ambient@claude-mods
claude plugin install dino@claude-mods
claude plugin install pomodoro@claude-mods
claude plugin install tycoon@claude-mods
```

Restart Claude Code after installing. The same works from inside a session with `/plugin marketplace add barisdemirhan/claude-mods` and `/plugin install <mod>@claude-mods`.

## The mods

| Mod | What it is | Start with |
| --- | --- | --- |
| [ambient](https://github.com/barisdemirhan/claude-ambient) | A living band above the prompt that Claude's work feeds, with sound: an aquarium, a bonsai, a skyline, a train and seven more scenes | `/ambient` |
| [dino](https://github.com/barisdemirhan/claude-dino) | A T-Rex runner in a pane, inspired by Chrome's offline game, with Claude's tool calls as the obstacles | `/dino` |
| [pomodoro](https://github.com/barisdemirhan/claude-pomodoro) | A pomodoro timer on the prompt's hint line whose break lands while Claude works, with a history and a report | `/pomodoro start` |
| [tycoon](https://github.com/barisdemirhan/claude-tycoon) | Token Tycoon, an idle game in a pane where Claude's tool calls earn the money | `/tycoon` |

Each mod's own README says what it does, key by key and hook by hook.

## Privacy

No mod here has analytics or an account, and none sends anything off your machine until you ask for the one thing in it that does. None reads a prompt's text, or a tool call's arguments or output.

| Mod | Reads of your session | Sends off your machine | Policy |
| --- | --- | --- | --- |
| ambient | Each tool call's name and whether it failed; when a turn starts and ends | Nothing, until you name a place for the weather scene. Then that place's name and coordinates go to [Open-Meteo](https://open-meteo.com/) | [PRIVACY.md](https://github.com/barisdemirhan/claude-ambient/blob/main/PRIVACY.md) |
| dino | Each tool call's name and whether it failed, while a run is on | Nothing, until you join the global top. Then your chosen name and your best runs' moves go to the author's server on Cloudflare | [PRIVACY.md](https://github.com/barisdemirhan/claude-dino/blob/main/PRIVACY.md) |
| pomodoro | When a turn starts and ends, where a prompt came from, and the name of the repository or folder | Nothing | [PRIVACY.md](https://github.com/barisdemirhan/claude-pomodoro/blob/main/PRIVACY.md) |
| tycoon | Each tool call's name and whether it failed; the output tokens a turn cost | Nothing, until you join the global top. Then your chosen name and your save go to the author's server on Cloudflare | [PRIVACY.md](https://github.com/barisdemirhan/claude-tycoon/blob/main/PRIVACY.md) |

What a mod keeps, it keeps in its own Claude Code store on your disk. What a mod's command answers is a row of the conversation, which Claude reads as it reads the rest. Each policy has the whole of it, and how to take your data off.

This repository itself is a list: it runs nothing and collects nothing.

## Requirements

- A Claude Code build with mod support (plugins that ship a hooks module). The mods are built and tested on 2.1.287 and 2.1.288. Mods sit behind a rollout switch, so if a mod's command does not show up after installing, the switch may still be off for you.
- The terminal or the desktop app.
- Sound needs macOS, where Claude Code has a player for it.

## If you installed a mod from its own marketplace

Each mod's repository is still a marketplace of its own (`dino@claude-dino` and the like), and installs from there go on getting updates. Nothing has to change.

Moving to `claude-mods` is a new install as Claude Code sees it, and starts with an empty store: without your scores, saves, rounds and settings, and without the secret that makes a name on a global top yours. To bring them along, copy the mod's store file to its new name before you install, with no Claude Code session open. For dino:

```sh
cp -R ~/.claude/plugins/store ~/claude-store-backup
cp ~/.claude/plugins/store/dino_claude-dino-98d7fb92c86a.json ~/.claude/plugins/store/dino_claude-mods-aeb35b495c33.json
claude plugin marketplace add barisdemirhan/claude-mods
claude plugin install dino@claude-mods
claude plugin uninstall dino@claude-dino
```

| Mod | Its store, installed from its own marketplace | Its store, installed from `claude-mods` |
| --- | --- | --- |
| ambient | `ambient_claude-ambient-abb626dfb229.json` | `ambient_claude-mods-c3eb600a5f3a.json` |
| dino | `dino_claude-dino-98d7fb92c86a.json` | `dino_claude-mods-aeb35b495c33.json` |
| pomodoro | `pomodoro_claude-pomodoro-69a776f141b5.json` | `pomodoro_claude-mods-cf0e3c48f8c2.json` |
| tycoon | `tycoon_claude-tycoon-ed96090b0132.json` | `tycoon_claude-mods-42ed3c337a0e.json` |

The files are in `~/.claude/plugins/store/`, where Claude Code 2.1.288 keeps a mod's store. The place is Claude Code's own and may change with it. The first line keeps a copy of every store in `~/claude-store-backup`, to put back if the move goes wrong. Uninstalling leaves the old store's file where it is.

Keep one of the two installs, not both: with both on, every hook runs twice.

## How it is put together

Each mod lives in its own repository, with its own issues, releases and license. This one holds only `.claude-plugin/marketplace.json`, which points at them.

```sh
claude plugin validate .
```

## License

MIT, for this list. Each mod carries its own license in its repository.
