# ACMElabs marketplace

Plugins from [ACMElabs](https://github.com/acmelabs-15), for three agent hosts.

## Use it

| Host | Command |
|:--|:--|
| Claude Code | `/plugin marketplace add acmelabs-15/marketplace` then `/plugin install brain@acmelabs` |
| Codex | `codex plugin marketplace add acmelabs-15/marketplace` then `codex plugin add brain@acmelabs` |
| Gemini CLI | `gemini extensions install https://github.com/acmelabs-15/brain` |
| Antigravity CLI | `agy plugin install https://github.com/acmelabs-15/brain.git` |

Gemini has no marketplace to add. It installs an extension straight from the plugin's own
repository.

## Plugins

| Plugin | What it does |
|---|---|
| [brain](https://github.com/acmelabs-15/brain) | A development lifecycle for coding agents: agent-skills wrapped with a glossary, plain talk, and one question at a time. For Claude Code, Codex, Gemini CLI and Antigravity CLI. |
| [jev-gate](https://github.com/acmelabs-15/jev-gate) | A PreToolUse gate: Jev scores each side-effecting tool call for destructive, exfiltration, secrets and off-task risk. Shadow mode logs only. For Claude Code only. |

### Retired

[ask-user-question](https://github.com/acmelabs-15/ask-user-question) was retired on
2026-10-28. Its skill ships in brain from v0.7.0, under the same name. Neither registry
lists it now. Claude Code's `renames` map in `.claude-plugin/marketplace.json` names it
`null`, so a user who still has it enabled sees that it was removed. Its repository says how
to move to brain.

## How this repo works

Each plugin lives in its own repository. This repo carries one registry file per host:

| File | Host |
|:--|:--|
| `.claude-plugin/marketplace.json` | Claude Code |
| `.agents/plugins/marketplace.json` | Codex |

Both name the plugin the same way:

```json
{ "source": "url", "url": "https://github.com/acmelabs-15/brain.git", "ref": "latest" }
```

The URL is written out in full rather than as `owner/repo` shorthand. Claude Code resolves that
shorthand to an SSH remote, which fails on a machine with no key loaded.

Both follow the `latest` tag. That tag lives in the plugin's repository and moves on every
release that is not a pre-release, so a release reaches all three hosts at once and this repo
needs no commit to publish one.

No entry carries a version string. The tag decides what installs, and a second copy of the
version here would go stale the moment a release ran.
