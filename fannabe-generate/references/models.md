# Choosing a model

List models per media type, then read the chosen model's schema before generating.

```bash
fannabe models list --media-type image      # image | video | audio | lip-sync
fannabe models schema <modelId>             # exact fields, defaults, and source slots
```

- The first column of `models list` is the model id you pass to `generate create`.
- Model ids are a stable public contract (e.g. `nano-banana-2-single-image`, `kling-2-6-motion-control`); prefer them over guessing.
- `models schema <id> --concept-type <type>` shows fields for a specific concept (e.g. `single-image`, `carousel`, `video-from-image`, `talking-video`). `--simple` shows the simple-mode fields.
- `economyMode` (a `--set economyMode=true` flag on supported models) trades priority for a lower price.

Pass `--concept-type <type>` on `generate create` so the request runs the intended concept rather than a generic default.
