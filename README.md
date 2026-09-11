# ACMElabs marketplace

Claude Code plugins from [ACMElabs](https://github.com/acmelabs-15).

## Use it

```
/plugin marketplace add acmelabs-15/marketplace
/plugin install ask-user-question@acmelabs
```

## Plugins

| Plugin | Version | What it does |
|---|---|---|
| [ask-user-question](https://github.com/acmelabs-15/ask-user-question) | 0.1.5 | Composes AskUserQuestion calls a human can answer on sight, and reads the replies that come back. |

## How this repo works

`.claude-plugin/marketplace.json` is the registry. Each plugin lives in its own repository and is
listed here with a `github` source, so a plugin's release cycle stays its own.

Each entry pins a `version`. A plugin's own pushes do not reach anyone until that string changes
here, so an update is a deliberate act rather than a side effect of a commit.
