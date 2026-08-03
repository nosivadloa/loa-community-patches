# Configurable secondary-stat scaling

Replaces a hardcoded secondary-stat gain gate with a formula based on the
configured individual skill and stat caps.

## Root cause

The stock condition `realStatLevel * 2 <= skillLevel` assumes a 100-point
skill cap and 50-point stat cap. On shards that raise the individual stat cap,
Wisdom and Will can become unable to gain naturally above 50.

## Fix

The eligibility ratio becomes:

```text
realStatLevel * (individualSkillCap / individualStatCap) <= skillLevel
```

With the native 100/50 caps, the behavior is unchanged. With 100/150 caps, a
100-point skill can support the full 150-point secondary stat range.

## Scope and application

- `scripts/globals/helpers/skills.lua`

```text
git apply --check secondary-stat-scaling.patch
git apply secondary-stat-scaling.patch
```

Restart after applying. Reverse with
`git apply -R secondary-stat-scaling.patch`.

## Validation

- Clean reverse-application check passed.
- Lua 5.1 syntax validation passed.
- The formula preserves native behavior at native cap values.
- Tested against LoA Eternal Dedicated Server game version `1.4.1.0`.
