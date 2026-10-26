# ROARR — technical architecture, separate repository snapshot

**Basis:** current `roarr.lua` and `roarr.toc`, inspected 2026-10-26. No actual game client was run.

## Call flow

```text
Configured action-bar slot pressed
  -> global UseAction wrapper
     -> ensureLoaded() once (ROARRDB -> local state)
     -> optional WATCH_MODE print
     -> watched slot matches?
        -> doBattleEmoteNow()
           -> ENABLED?
           -> GetTime() beyond BATTLE_COOLDOWN?
           -> update LAST_BATTLE_EMOTE_TIME
           -> math.random(1,100) <= battle_chance?
              -> pick one of 5 tokens
              -> DoEmote(token) or fallback EMOTE text
     -> delegate to previously captured _Orig_UseAction
```

**Timing nuance:** last-attempt time is updated *before* the chance roll. Even a failed roll blocks further checks until cooldown expires. `LAST_BATTLE_EMOTE_TIME` starts at zero, so eligibility of the first press depends on game uptime.

## Configuration

| Symbol / key | Default | Purpose |
| --- | --- | --- |
| `WATCH_SLOT` / `ROARRDB.slot` | unset | Action slot to monitor |
| `WATCH_MODE` | false | Temporary slot-number printout; not persisted |
| `battle_chance` / `ROARRDB.battle_chance` | 100 | Chance 0–100 |
| `BATTLE_COOLDOWN` / `ROARRDB.battle_cd` | 6 | Nonnegative seconds, no enforced maximum |
| `ENABLED` / `ROARRDB.enabled` | true | On/off preference |
| `LAST_BATTLE_EMOTE_TIME` | 0 | Session-local last eligible attempt |
| `EMOTE_TOKENS_BATTLE` | five tokens | Fixed source table |

`ROARRDB` is declared by the TOC as **SavedVariables** (account-wide, not character-specific). On the first action press or slash command, `ensureLoaded` initializes in-memory state. `PLAYER_LOGIN` only seeds the pseudo-random generator; `PLAYER_LOGOUT` writes current local state to the DB.

**Potential state-loss edge case:** logging in and out without any action or slash command may write initial/default values over a previously saved configuration, because login does not call `ensureLoaded`. This is a **static risk**, not a reproduced error.

## Slash commands

`/roarr` uses Lua `string.find`, `string.gsub` and `tonumber` to parse commands. It implements `slot`, `watch`, `chance`, `cd`, `on`, `off`, `info`, `reset`, `save`, and `tutorial`. The unique source change in this repo is the longer multi-line tutorial.

The slot command accepts any numeric value without checking legal bar-slot bounds or integer requirements; chance is constrained to 0–100; cooldown is constrained to be nonnegative.

## Dependencies, packaging and runtime

- Files: `roarr.lua`, `roarr.toc`; manifest interface `11200`, version `1.0`, author Babuni.dev.
- Uses standard WoW addon events `PLAYER_LOGIN` and `PLAYER_LOGOUT`; no update-loop scheduler.
- Built-in game `DoEmote` tokens are the only emote selection content.
- No custom sound/media resources, no cross-addon protocol, no sync layer or GUI.
- Global `UseAction` hook may interact with other addons; event/cast success is not checked.

## Comparison to `babunidev/roar`

The present `roarr.lua` and that repo's present `roarr.lua` are **identical after excluding the `tutorial` branch**. This direct content comparison is stronger than inferring a fork from project names. Both manifests presently match and declare the same account-wide `ROARRDB`.

This is not proof of a formal fork decision, release lineage or authoritative distribution choice. The expanded tutorial is the source-observed differentiator.
