# Enable township marketplace boards

Removes the stock early-return guard that disables the otherwise implemented
township marketplace-board interface.

## What changes

- Deletes the hardcoded "Marketplace boards are disabled for now" response.
- Allows the existing proximity, township, listing, purchase, and window logic
  beneath that guard to run unchanged.

## Scope

- `scripts/globals/mobile_effects/players/marketplace_board.lua`

This is an optional feature-enablement patch, not a claim that marketplace
boards suit every shard economy. Test listing creation, purchase, expiry, and
permissions before production deployment.

## Apply

From the directory containing `scripts`:

```text
git apply --check marketplace-boards-enable.patch
git apply marketplace-boards-enable.patch
```

Restart the server after applying. Reverse with:

```text
git apply -R marketplace-boards-enable.patch
```

## Verification checklist

1. Open a township marketplace board as a valid township member.
2. Create and cancel a listing.
3. Purchase a listing with another account.
4. Confirm expired listings and permission failures behave correctly.

## Validation

- Applies cleanly to untouched LoA Eternal Dedicated Server `1.4.1.0` stock.
- Lua 5.1 syntax validation passed.
- The patch changes only the stock disable guard.
