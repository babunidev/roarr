# ROARR — roadmap / verification backlog

**Author:** Babuni.dev  
**Status:** proposed validation and questions for the creator. None is an approved new feature.

## Current documented baseline

- `roarr.lua` and `roarr.toc`, version **1.0**, interface `11200`.
- One watched `UseAction` slot; five built-in emotes; configurable chance, cooldown, and on/off switch.
- Account-wide `ROARRDB` storing `slot`, `battle_cd`, `battle_chance`, `enabled`.
- Expanded seven-step `/roarr tutorial`—the only difference identified in the current Lua code relative to the current source of the separate `roar` repo.
- No automated tests included in the inspected tree.

## Verify the existing addon first

1. Install the committed `roarr` package on a target 1.12-compatible client and confirm loading and slash registration.
2. Run `/roarr tutorial` and check all **seven numbered messages** for readability and correctness.
3. Use watch mode to find a slot; set and reset it; confirm actions still fire when the wrapper delegates to `UseAction`.
4. Test all five built-in emotes and the effects of `/roarr chance 0`, `40`, `100`, plus `/roarr cd 0` and a higher interval.
5. Verify that missed probability rolls consume cooldown, as the current source dictates.
6. Confirm on/off behavior, saved settings through `/reload` and a fresh login, and account-wide behavior on multiple characters.
7. Test the possible **uninitialized logout overwrite** case: log in and log out without using slash commands or action bars after previously saving nondefault values.
8. Test coexistence with `BuxbrewCharge`, `roar` and other addons that wrap `UseAction`; do not install duplicate ROARR packages together without controlling the test.
9. Record observations, client build, Lua errors, related addon load order and tested commit.

No live-client tests were performed by the 2026-10-26 documentation work.

## Creator decisions to make later

- Should `roarr` be the primary public repo, while `roar` remains an archived historical prototype?
- Should the two repositories remain separate or eventually be consolidated? **No merge or deletion is implied.**
- Is the longer tutorial sufficient, or should there be a non-spamming preview and more explicit first-use guidance?
- Should a failed chance roll consume cooldown?
- Should watched slots be per-character rather than account-wide?
- Does the historical MIT copyright attribution require clarification?

All of these are **open questions**, not silently accepted improvements.
