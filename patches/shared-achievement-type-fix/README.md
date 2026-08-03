# LoA shared achievement-type claim fix

This patch fixes unclaimable achievement notifications when multiple title
series share one achievement `Type`. The stock data places both the Mage and
Evoker series under `MagerySkill`, while the Achievements window collapses the
entire type into one row.

## Symptoms

- A persistent `!` appears on the Achievements button and Skill tab.
- The visible Mage/Evoker row does nothing when clicked.
- The row may display a completed Mage rank while an Evoker rank is waiting.
- The Magery row has no achievement icon.

## Root cause

`CompleteAchievementPressed` compares the visible row name with the next
achievement name in the static array. That assumption fails when one `Type`
contains multiple series or duplicate thresholds. It can also dereference a
missing `tab[i + 1]` at the final entry.

The fix claims the first server-earned `AchievementWaiting` entry matching the
selected category, type, and subcategory. It does not grant arbitrary rewards:
the entry must already exist in the player object's server-side waiting list.

The patch also maps the legacy `MagerySkill` type to the existing
`ManifestationSkill` or `EvocationSkill` client icon according to the displayed
title.

## Apply directly to the base scripts

From the directory containing the `scripts` folder:

```text
git apply --check loa-shared-achievement-type-fix.patch
git apply loa-shared-achievement-type-fix.patch
```

Back up the original file first if the server files are not under version
control.

## Apply as a mod override

Apply the patch to a copy of the stock file, then place the patched file at:

```text
<ModName>/scripts/base_player_achievement.lua
```

Restart the server after installing the override. Players with several pending
ranks claim them one at a time by clicking the marked row until the `!` clears.

## Compatibility and verification

- Target file: `scripts/base_player_achievement.lua`
- Tested with Lua 5.1 syntax validation.
- Tested against a stock file with SHA-256:
  `709138D2CAEFCB15CD76284C2EFB5ADDAE48F1B8A29D3E33408501099E1F3311`
- Expected client textures:
  `achievement_Skill_ManifestationSkill` and
  `achievement_Skill_EvocationSkill`.

If `git apply --check` reports a context mismatch, port the two hunks manually
instead of replacing the whole file; this preserves any unrelated server
customizations.
