# Profession-rank enforcement

Connects combat profession ranks to ability-book consumption, training,
hotbar availability, and ability execution.

## Symptoms

The stock helper contains profession concepts, but higher-tier combat ability
books and actions can bypass the intended earned-rank progression.

## Changes

- Defines the required profession tier for combat abilities.
- Blocks ability execution when the matching rank has not been earned.
- Disables and annotates locked hotbar actions.
- Blocks training and ability-book consumption until the required tier.
- Rechecks the requirement when a delayed book-use response completes.

## Scope

- `scripts/globals/helpers/prestige.lua`
- `scripts/prestige_ability_book.lua`

## Apply

```text
git apply --check profession-rank-enforcement.patch
git apply profession-rank-enforcement.patch
```

Apply from the directory containing `scripts`, then restart the server.

## Rollback

Use `git apply -R profession-rank-enforcement.patch` and restart. The patch
does not delete learned abilities or profession progress.

## Validation

- Clean reverse-application check passed.
- Both Lua files pass Lua 5.1 syntax validation.
- Tested against LoA Eternal Dedicated Server game version `1.4.1.0`.
