# Unrestricted sewer teleporter

Allows the stock sewer teleporter to activate regardless of the player's
legacy `PickedProfession` state.

## Root cause

The stock script redirects players without a selected profession through
`NewbieLeaveTown` instead of activating the teleporter. Shards that repurpose
the sewers as onboarding or general content can therefore strand or redirect
otherwise eligible players.

## Changes

- Removes the `PickedProfession` gate.
- Preserves normal activation and administrator destination-setting behavior.

## Scope

- `scripts/sewer_teleporter.lua`

This is an optional progression-rule change. Do not apply it if profession
selection is intentionally required before leaving the starter flow.

## Apply

From the directory containing `scripts`:

```text
git apply --check unrestricted-sewer-teleporter.patch
git apply unrestricted-sewer-teleporter.patch
```

Restart the server after applying. Reverse with:

```text
git apply -R unrestricted-sewer-teleporter.patch
```

## Verification checklist

1. Activate the sewer teleporter with `PickedProfession` false or unset.
2. Activate it with a selected profession.
3. Confirm "Set Destination" still opens its normal window for authorized use.

## Validation

- Applies cleanly to untouched LoA Eternal Dedicated Server `1.4.1.0` stock.
- Lua 5.1 syntax validation passed.
- No destination or access-control logic beyond the profession gate changes.
