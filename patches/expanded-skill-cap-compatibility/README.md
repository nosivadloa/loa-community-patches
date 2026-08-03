# Expanded total-skill-cap compatibility

Makes two stock systems behave predictably when a shard raises the total player
skill cap above the native 600 points.

## Root cause

- NPC quest shouts use a hardcoded `< 600` eligibility check, so trained
  characters stop receiving quest notifications even when the configured cap
  is higher.
- Dynamic proximity spawns use the configured total cap as player power. A cap
  increase intended only to permit broader builds can therefore accelerate
  nearby spawns unintentionally.

## Changes

- NPC quest-shout eligibility follows `PlayerSkillCap.Total`.
- Adds `DynamicSpawnPowerSkillCap`, defaulting to the native 600-point balance
  ceiling.
- Dynamic spawn power uses the lower of the configured total cap and the
  dedicated spawn-power ceiling.

## Scope

- `scripts/base_ai_npc.lua`
- `scripts/globals/helpers/spawns.lua`
- `scripts/globals/server_settings/skills.lua`

The patch does **not** raise skill caps or alter skill-gain rates. Operators set
`PlayerSkillCap.Total` separately. Raise `DynamicSpawnPowerSkillCap` too only
when additional trained skills should increase dynamic spawn pressure.

## Apply

From the directory containing `scripts`:

```text
git apply --check expanded-skill-cap-compatibility.patch
git apply expanded-skill-cap-compatibility.patch
```

Restart the server after applying. Reverse with:

```text
git apply -R expanded-skill-cap-compatibility.patch
```

## Verification checklist

1. Set `PlayerSkillCap.Total` above 600 on a test shard.
2. Confirm a character between 600 and the new cap still receives relevant NPC
   quest shouts.
3. Confirm dynamic proximity spawn pacing remains at the desired 600-point
   ceiling.
4. Change `DynamicSpawnPowerSkillCap` and confirm spawn pacing follows it.

## Validation

- Applies cleanly to untouched LoA Eternal Dedicated Server `1.4.1.0` stock.
- All three Lua files pass Lua 5.1 syntax validation.
- Default 600-point shards retain their original effective behavior.
