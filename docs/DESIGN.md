# ROARR — interaction and onboarding design

**Creative author:** Babuni.dev.

## Core emotional effect

The addon attaches a playful expression to the player's existing action-bar behavior. ROAR or CHARGE can punctuate aggression; CHEER celebrates; FLEX shows swagger; BORED interrupts the battle with a comic contrast. A short pool of game-native emotes keeps the behavior simple and immediately recognizable.

The player still decides what to press. The addon does not control movement, attacks, targeting or combat priorities.

## The seven-step tutorial: this repo's distinct iteration

The previous ROARR implementation in `babunidev/roar` contains only a compact `tutorial` command summary. In this repository, commit `4fc6a68` on **2025-11-23** replaced that summary with **seven numbered messages**:

1. Toggle slot watch and press buttons.
2. Assign a watched slot.
3. Set a chance percentage.
4. Set a cooldown.
5. Switch the addon on or off.
6. Inspect current configuration.
7. Save settings.

The purpose can be reasonably read as easier **first-use guidance**, especially for someone unfamiliar with action-slot numbers. That interpretation is an editorial reading of code; the original creator discussion explaining the change is not available.

## Text-first experience

The user configures the addon through `/roarr` commands; a red `ROARR:` prefix distinguishes feedback in the chat frame. There is no graphics panel, animation editor or tutorial popup. The original source has a short sample command sequence in README, and the expanded source tutorial can be run on demand.

The `watch` toggle prints every captured action ID while enabled; turning it off keeps later play quieter. The `on`/`off` toggle allows a reversible pause without wiping the chosen slot.

## Emote cadence

Default cooldown: **6 seconds**. Default proc chance: **100%**. After a valid slot press, the enabled/cooldown checks run; the clock is updated before chance is sampled. This means `chance 40` and `cd 12` provide at most one 40% roll per 12-second cooldown opportunity, not one roll on each press.

## Limitations and accessibility checks

Many on-screen status lines make the tutorial readable but potentially noisy; test this in live chat. English command descriptions and fixed token names may depend on client locale. If the slot changes when the action bar layout changes, the player must update `/roarr slot`. Input validation currently accepts noninteger numeric slot values. Actual usability and compatibility remain to be tested.
