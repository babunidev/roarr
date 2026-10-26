# ROARR repository — development rules

**Creative author:** Babuni.dev.

## Read before changing anything

Review `README.md`, `CONCEPT.md`, `docs/DEVLOG.md`, `docs/DECISIONS.md`, `roarr.lua`, `roarr.toc` and the separate `roar` repository only when making a comparison. This repository is **`babunidev/roarr`**, not `babunidev/roar`; do not edit the other repo accidentally.

## Preserve provenance

1. Attribute the project's purpose, character direction and any approved creative choices to Babuni.dev.
2. Credit AI for identifiable analysis, suggestions, authored code or documentation separately. Do not infer who conceived a feature merely from a source file.
3. Treat the November 2025 seven-step tutorial revision as a documented implementation difference, not proof of an unseen approval discussion.
4. Keep the two GitHub histories separate. Never merge, rename, archive or delete one without explicit direction.
5. Keep historical MIT license attribution intact. Existing copyright line `2025 Elexior` is a rights statement, not disposable display branding.
6. Every substantial implementation requires a changelog, narrative devlog, decision/update record and accurate test results. Retrospective inference must be labeled.

## Engineering constraints

- Target WoW 1.12/Lua 5.0-compatible APIs unless Babuni.dev directs otherwise.
- Preserve original action execution when intercepting `UseAction`.
- Understand that a missed chance roll consumes cooldown under current code.
- `ROARRDB` is account-wide, but lazily loaded; test no-interaction logout carefully.
- Ensure emote tokens exist on the target client before claiming support.
- Do not manufacture gameplay test results from source inspection.
- Keep all secrets and private player chats out of public documentation.

The 2026-10-26 work was documentation-only and did not approve runtime changes.
