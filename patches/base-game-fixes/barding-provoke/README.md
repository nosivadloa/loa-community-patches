# Barding and Provoke repair

Repairs the stock Provoke flow and makes it train the visible, cap-counted
`BardSkill` instead of hidden legacy Provocation.

## Corrected behavior

- Musicianship receives the correct skill level and gain chance.
- A successful performance always requests the second target.
- Barding is checked once after both targets are valid.
- Difficulty uses the average of the two creatures rather than the stock
  sum-plus-half calculation that can exceed the 100 skill cap.
- Successful Provoke adds threat toward the selected victim, not the bard.
- The instrument lockout matches the displayed one-second cooldown.
- Target range and line-of-sight failures return clear feedback.
- A per-action gain multiplier allows Provoke practice to compensate for its
  Musicianship gate without changing the global gain rate.
- Stock creatures inheriting the default difficulty of 100 can be tiered from
  attack and maximum health instead of making harmless wildlife equal bosses.

## Scope

- `scripts/globals/mobile_effects/skills/bard/provoke.lua`
- `scripts/globals/helpers/skills.lua`

## Operator review required

Review `GetBardingDifficulty` before deployment. If your shard marks custom
bosses with object variables, add those predicates and return `100` before the
inferred power calculation. Deliberately authored values from 1-99 are
preserved; the stock inherited value of 100 is treated as a fallback.

This portable patch does not migrate previously earned hidden Provocation
values. A shard with existing players should implement a one-time migration to
retain the greater of legacy Provocation and visible Barding.

## Apply and rollback

```text
git apply --check barding-provoke.patch
git apply barding-provoke.patch
```

Restart after applying. Roll back with `git apply -R barding-provoke.patch`.

## Validation

- Clean reverse-application check passed.
- Both Lua files pass Lua 5.1 syntax validation.
- The public patch contains no Nosivad-specific object-variable names.
- Tested against LoA Eternal Dedicated Server game version `1.4.1.0`.
