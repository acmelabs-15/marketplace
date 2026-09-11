# ACMElabs marketplace

Plugins from [ACMElabs](https://github.com/acmelabs-15), for three agent hosts.

## Use it

| Host | Command |
|:--|:--|
| Claude Code | `/plugin marketplace add acmelabs-15/marketplace` then `/plugin install ask-user-question@acmelabs` |
| Codex | `codex plugin marketplace add acmelabs-15/marketplace` then `codex plugin install ask-user-question` |
| Gemini CLI | `gemini extensions install acmelabs-15/ask-user-question` |

Gemini has no marketplace to add. It installs an extension straight from the plugin's own
repository.

## Plugins

| Plugin | What it does |
|---|---|
| [ask-user-question](https://github.com/acmelabs-15/ask-user-question) | Composes AskUserQuestion calls a human can answer on sight, and reads the replies that come back. |

## How this repo works

Each plugin lives in its own repository. This repo carries one registry file per host:

| File | Host | Points at the plugin with |
|:--|:--|:--|
| `.claude-plugin/marketplace.json` | Claude Code | `{"source": "github", "repo": "...", "ref": "latest"}` |
| `.agents/plugins/marketplace.json` | Codex | `{"source": "url", "url": "...", "ref": "latest"}` |

Both follow the `latest` tag. That tag lives in the plugin's repository and moves on every
release that is not a pre-release, so a release reaches all three hosts at once and this repo
needs no commit to publish one.

No entry carries a version string. The tag decides what installs, and a second copy of the
version here would go stale the moment a release ran.
