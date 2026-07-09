# Fannabe Skills

Agent skills for [Fannabe](https://www.fannabe.com) — generate images, videos, and voice for your AI models from any skill-capable agent (OpenClaw, Hermes, Claude Code, Cursor, Codex).

The skills wrap the [`@fannabe/cli`](https://www.npmjs.com/package/@fannabe/cli), so once installed you can just say: **"Generate an image with Fannabe."**

Prefer a native MCP connection? Use the [`@fannabe/mcp`](https://www.npmjs.com/package/@fannabe/mcp) server instead — this repo is the CLI-based skill path recommended for shell-driven agents.

## Skills

| Skill | What it does |
| --- | --- |
| [`fannabe-generate`](fannabe-generate/SKILL.md) | Generate/edit images and videos, image-to-video, motion control, character swap, prompt tools, captions, downloads |

## Install

**OpenClaw** (or any agent, via git):

```bash
openclaw skills install git:Fanzilla-Technologies/fannabe-skill@main
```

**Hermes / skills.sh** (`npx skills`):

```bash
npx skills add Fanzilla-Technologies/fannabe-skill
```

**Claude Code / Cursor / Codex**: add this repo as a plugin marketplace (`.claude-plugin`, `.cursor-plugin`, `.codex-plugin` manifests are included), or point your agent's skills directory at a checkout of this repo.

See [INSTALL.md](INSTALL.md) for per-agent details.

## Sign in

```bash
npm install -g @fannabe/cli
fannabe auth login
```

Opens a browser once; the token caches in `~/.fannabe`. Generations spend Fannabe credits from your account.

## License

MIT — see [LICENSE](LICENSE). The skill contains usage instructions only; Fannabe itself is a hosted service governed by its [Terms of Service](https://www.fannabe.com/terms-of-services).
