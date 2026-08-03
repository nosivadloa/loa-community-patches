# Profession progression repair

Repairs the stock profession quest chains that cannot progress because later
tiers are unconditionally disabled or their trainer/objective data is broken.

## Symptoms

- Eligible players receive a generic refusal after completing tier I.
- Mage, Fighter, or Rogue trainers omit required later-tier dialogue.
- Some objectives cannot advance because their state key or return marker is
  misspelled or undefined.

## Root cause and changes

Several authored tier II-IV quests contain unconditional `Disabled`
requirements. The patch removes only those gates while retaining the previous
tier, skill threshold, one-time completion, objective, and reward rules.

It also adds missing Mage/Fighter/Rogue trainer steps and corrects the known
copy/paste objective keys and return markers. Blacksmith required no override.

## Scope

- `scripts/ai_prestige_trainer.lua`
- 41 profession quest files under
  `scripts/globals/static_data/quests/`

The affected families are Alchemist, Bard, Carpenter, Chef, Fighter, Fisher,
Lumberjack, Mage, Miner, Rogue, Scribe, Tailor, and Tamer.

## Apply

From the directory containing `scripts`:

```text
git apply --check profession-progression.patch
git apply profession-progression.patch
```

For a mod override, copy the corresponding stock files into the same relative
paths in the mod first, then apply the patch there. Restart the server.

## Rollback

Reverse the diff with `git apply -R profession-progression.patch` and restart.
Existing completed profession progress is not reset by applying or removing
the script changes.

## Validation

- Clean reverse-application check passed against the tested modified tree.
- All 42 Lua files pass Lua 5.1 syntax validation.
- Tested against LoA Eternal Dedicated Server game version `1.4.1.0`.
