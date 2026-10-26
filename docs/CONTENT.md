# ROARR — in-game words, built-in emotes and tutorial

**Author:** Babuni.dev.  
**Source:** `roarr.lua`.

## Five built-in emote tokens

| Token | Player-facing flavor |
| --- | --- |
| `ROAR` | A fierce, loud interruption |
| `CHARGE` | Momentum and battle spirit |
| `CHEER` | Encouragement/celebration |
| `BORED` | Wry comic contrast |
| `FLEX` | Strength and bravado |

The game client supplies the exact animation or rendered emote wording for these built-in tokens. ROARR does not embed five original audio recordings, custom animations or five custom text scripts.

Fallback when `DoEmote` is unavailable: `SendChatMessage("makes a battle cry!", "EMOTE")`. The fallback is written in the addon; whether it is needed/allowed on a particular server is unverified.

## Tutorial text

This snapshot's unique added content is an expanded `/roarr tutorial` sequence. Rather than one compact hint, it prints a **title** and **seven numbered steps** about watch, slot, chance, cooldown, on/off, info and save. It is authored directly in `roarr.lua`, not loaded from an external content or localization file.

## Configuration/status messages

The chat UI prints `ROARR:` plus descriptions for enabled, disabled, watched slot, saved settings, errors and `info`. This source supports English-only author-supplied guidance. Localization of Blizzard's built-in emote output is controlled by the game, not by this addon.

For future content revisions, preserve authorship and distinguish the creator's source text from the game-owned built-in emote tokens. Record specific accepted changes and tested behavior rather than silently replacing content.
