# Installing the Fannabe skill

All paths wrap the same [`@fannabe/cli`](https://www.npmjs.com/package/@fannabe/cli). Install and sign in once:

```bash
npm install -g @fannabe/cli
fannabe auth login
```

## OpenClaw

From ClawHub (once published) or directly from git:

```bash
openclaw skills install git:Fanzilla-Technologies/fannabe-skill@main
# global (all local agents):
openclaw skills install git:Fanzilla-Technologies/fannabe-skill@main --global
```

## Hermes / skills.sh (`npx skills`)

GitHub is the registry — no submission step:

```bash
npx skills add Fanzilla-Technologies/fannabe-skill
```

## Claude Code

Add this repo as a plugin marketplace (it ships `.claude-plugin/marketplace.json` and `plugin.json`), or clone it into a directory your skills config already scans. The skill is then invocable as `/fannabe:generate`.

## Cursor / Codex

`.cursor-plugin/plugin.json` and `.codex-plugin/plugin.json` are included so the repo installs as a plugin in each. Otherwise, any agent with shell access can use the skill by reading `fannabe-generate/SKILL.md`.

## Environments

Point at a non-production API with `FANNABE_API_URL=<url>`, and keep that login separate with `FANNABE_CONFIG_DIR=~/.fannabe-staging`. Both are environment variables read by the CLI.
