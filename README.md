# spec-kit-preset-toc-navigation

A [Spec Kit](https://github.com/github/spec-kit) preset that adds a navigable Table of Contents to generated `spec.md`, `plan.md`, and `tasks.md` documents.

## What it does

- Adds a `## Table of Contents` section with GitHub-style anchor links to all three structure templates
- Instructs the `/speckit.specify`, `/speckit.plan`, and `/speckit.tasks` commands to generate and maintain the TOC from final `##`-level headings

## Installation

```bash
specify preset add --from https://github.com/Quratulain-bilal/spec-kit-preset-toc-navigation/archive/refs/tags/v1.0.0.zip
```

## What gets overridden

| Type | Name | Description |
|------|------|-------------|
| Template | spec-template | Adds TOC with anchors including `-mandatory` suffix |
| Template | plan-template | Adds TOC after metadata, before Summary |
| Template | tasks-template | Adds TOC with anchors for stable headings, plain text for dynamic phases |
| Command | speckit.specify | TOC generation instruction with self-reference exclusion and clarify stale TOC handling |
| Command | speckit.plan | TOC generation instruction before Summary |
| Command | speckit.tasks | TOC generation instruction with implement.md misparse warning |

## Design decisions

- Only `##`-level headings included to keep TOC concise
- Standard GitHub anchor format (lowercase, spaces to hyphens, strip special characters)
- Dynamic phase headings (Phase 3-5) use plain text in template TOC since actual titles are generated at runtime
- `## Table of Contents` does not link to itself (self-reference exclusion)
- Commands instruct the AI to regenerate TOC after `/speckit.clarify` rewrites
- Downstream consumers (`/speckit.implement`, `/speckit.analyze`) are warned that TOC is navigational only

## Requirements

- Spec Kit >= 0.4.0

## License

MIT
