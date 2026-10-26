# ROARR — action-slot battle emotes

**Author / creative director:** Babuni.dev  
**Repository:** `babunidev/roarr`  
**Client target declared in source:** World of Warcraft 1.12 / interface `11200`  
**Addon version:** 1.0  
**Verification:** Static repository inspection; not tested in-game during this documentation pass.

ROARR makes an ordinary action-bar button a chance for spontaneous roleplay. The addon watches one configured action slot, and after checking its enable switch, cooldown and probability, it chooses one of five built-in game emotes: **ROAR, CHARGE, CHEER, BORED, FLEX**. The underlying action is still forwarded to World of Warcraft.

This is a small **expressive addon**, not automatic combat decision-making, a scripted ability rotation, or a source of custom voice/animation assets.

## Install and try it

Install both files in the game’s addon directory:

```text
Interface/
└── AddOns/
    └── roarr/
        ├── roarr.toc
        └── roarr.lua
```

Restart the game and enable ROARR. The client must support the addon’s 1.12-era APIs; live compatibility has not been verified by this review.

1. Run `/roarr tutorial` to read the addon’s seven-step setup guide.
2. Run `/roarr watch`, then press the button whose slot you want to learn.
3. Enter `/roarr slot 3` (replace `3` with the reported slot number).
4. Turn the watch messages off with `/roarr watch`.
5. Optionally set `/roarr chance 40`, `/roarr cd 12`, and `/roarr on`.

### Command reference

| Command | Current source behavior |
| --- | --- |
| `/roarr tutorial` | Print the extended seven-step setup guide |
| `/roarr watch` | Toggle reporting of pressed action slot numbers |
| `/roarr slot <number>` | Select and save the watched slot |
| `/roarr chance <0-100>` | Set the percent chance of an emote at an eligible attempt |
| `/roarr cd <seconds>` | Set a cooldown of zero or greater; no fixed maximum |
| `/roarr on` / `/roarr off` | Enable or disable responses without clearing saved settings |
| `/roarr info` | Show slot, chance, cooldown, enabled status and pool size |
| `/roarr reset` | Clear the selected action slot |
| `/roarr save` | Save current settings to the account-wide `ROARRDB` |

Defaults are **on**, **100% chance**, a **6-second cooldown**, and no configured slot.

**Important timing detail:** The code updates its cooldown timestamp **before** the chance roll. A failed 40% roll still consumes the cooldown interval. This is a source observation, not a proposal to change gameplay.

## Relationship to `babunidev/roar`

There are **two separate GitHub repositories**. The [older `roar` repository](https://github.com/babunidev/roar) went through ROAR/ROARR renaming experiments on **November 22–23, 2025** and already contained the same core ROARR system. This repository, `roarr`, was first uploaded on **November 23, 2025**, with the same addon configuration and gameplay code, and shortly afterward gained a longer `/roarr tutorial`.

In the currently committed versions, the **Lua files are identical apart from that tutorial branch**. The Git history supports a closely related second repository snapshot, but does **not** establish why the creator maintained two repos or which should be the authoritative distribution. Neither repo was merged, deleted or redirected during this documentation work.

ROARR also must not be confused with the separate, more advanced **RoarForever** project without an explicit creator-approved relationship.

## Scope and limitations

- An emote is attempted on **button press**, not after successful casting or entering combat.
- `DoEmote` uses built-in game tokens. A text fallback is used if that API is absent.
- The code wraps global `UseAction`; other addons doing the same may create load-order interactions.
- Configurations are saved **account-wide**, even if characters use different action bars.
- The saved state is loaded lazily. The logout handler may overwrite stored values with defaults if the player never uses a hooked action or command during the session; this is a risk identified from source, not a tested failure.
- Although the source declares Lua 5.0 compatibility, actual client behavior must be verified before making a broad support claim.

## License and author credit

**Project author:** Babuni.dev. The repository includes an MIT `LICENSE` with a historic copyright notice for **Elexior (2025)**. The notice has deliberately **not been changed**; this review does not establish whether the historical name and current author credit identify the same rights holder. The license file governs distribution rather than the informal “shout into the void” wording of the earlier README.

## Development documentation

- [Concept](CONCEPT.md) · [Interaction design](docs/DESIGN.md) · [Emote/content inventory](docs/CONTENT.md)
- [Architecture](docs/ARCHITECTURE.md) · [Decision evidence](docs/DECISIONS.md) · [Development journal](docs/DEVLOG.md)
- [Roadmap](ROADMAP.md) · [Changelog](CHANGELOG.md)
- [Human–AI collaboration](docs/AI_COLLABORATION.md) · [Developer instructions](AGENTS.md)
