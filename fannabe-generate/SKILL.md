---
version: 0.1.2
name: fannabe-generate
description: |
  Generate images, videos, and voice for your AI characters via Fannabe.
  Use when: "generate an image", "make a video of my character",
  "animate this photo", "image-to-video", "motion control / transfer this
  dance onto my character", "character swap", "edit/restyle this image",
  "caption this video", "improve/rewrite this prompt", "describe this photo
  as a prompt", "show my gallery", "download my latest render", or
  "how many credits do I have". Wraps the `fannabe` CLI, which runs the same
  models, settings, and credit pricing as the Fannabe web studio.
  NOT for: training new characters (done in the web studio), or non-Fannabe
  providers.
argument-hint: "[what-to-generate] [--character <name-or-id>] [--model <id>]"
homepage: https://www.fannabe.com
allowed-tools: Bash
metadata:
  {
    "openclaw":
      {
        "requires": { "bins": ["node"] }
      }
  }
---

# Fannabe Generate

Create AI-character images, videos, and voice from the terminal. This skill drives the `fannabe` CLI, which talks to the Fannabe API and spends the signed-in user's credits.

## Step 0 — Bootstrap (before anything else)

1. If `fannabe` is not on `$PATH`, install it:
   ```bash
   npm install -g @fannabe/cli
   ```
2. If a command fails with a "Not logged in" / 401 error, ask the user to run `fannabe auth login` (opens a browser) and wait for confirmation. The token is cached in `~/.fannabe`.

Every command supports `--help`, and output is plain text meant to be parsed.

## Core workflow

```bash
fannabe characters list                       # pick a character (id, name, appearance)
fannabe models list --media-type image        # pick a model (first column is the id)
fannabe models schema <modelId>               # discover that model's fields + source slots
fannabe generate create <modelId> \
  --character <characterId> --media-type image \
  --prompt "golden hour rooftop portrait, cinematic" \
  --set aspectRatio=9:16 --set resolution=1k \
  --wait --download ./output                  # prints cost, blocks until done, saves the file
```

- Match the user's wording to a character with `fannabe characters list --search "<text>"` (matches name and appearance, e.g. "redhead").
- Set any model field with repeatable `--set key=value` (see `models schema <id>`), or a full `--settings '<json>'`.
- Preview spend first with `fannabe generate cost <modelId> --media-type image --character <id> --set resolution=1k`.

## When the user describes an outfit or scene in plain words

Prefer the curated Theme/Outfit presets over a long hand-written prompt. See [references/easy-mode.md](references/easy-mode.md).

## Image-to-video, edits, motion control, character swap

These attach source media to model slots. The two id kinds are NOT interchangeable. See [references/source-media.md](references/source-media.md).

## Prompt assistance

`fannabe prompt improve|ai-edit|from-image`, or inline `--enhance-prompt` / `--from-image` / `--ai-edit`. See [references/prompt-tools.md](references/prompt-tools.md).

## Async jobs and downloads

```bash
fannabe jobs list --ongoing
fannabe jobs wait <taskId> --timeout 15m
fannabe jobs download <taskId> --output ./output/result.mp4
fannabe caption-on-video <videoContentId> --text "..." --character <id>
fannabe video frame <videoContentIdOrFile> --time 1.5 --upload   # still frame -> imageId
```

## Costs and account

Priced in Fannabe credits, identical to the web studio. `fannabe account` shows the balance.

## References (read as needed)

- [references/models.md](references/models.md) — choosing a model per media type
- [references/easy-mode.md](references/easy-mode.md) — Theme/Outfit presets
- [references/source-media.md](references/source-media.md) — source slots, the two id kinds, motion control, character swap
- [references/prompt-tools.md](references/prompt-tools.md) — prompt improve / AI edit / from-image
- [references/troubleshooting.md](references/troubleshooting.md) — auth, environments, common errors

## Rules for agents

- Generation is async: only completed jobs have downloadable media; use `--wait` or `jobs wait`.
- Never guess model fields — read `models schema <id>` and `--help`.
- The estimated cost prints before every generation; surface it to the user for anything non-trivial.
