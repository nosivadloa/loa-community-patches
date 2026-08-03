# Merchant purchasing repair

Repairs quantity selection, interaction-range checks, and multi-item stock
consumption in the merchant shop UI.

For quantity controls without the interaction-range changes, use the narrower
[`merchant-quantity-selection`](../merchant-quantity-selection/) patch. Do not
apply both because their quantity hunks overlap.

## Symptoms

- Quantity text fields in object-bound shop windows do not reliably reach the
  server.
- A shop opened from a display item or sale animal can fail checkout because
  distance is rechecked against the merchant mobile instead of the interaction
  anchor.
- Multi-quantity non-stackable purchases can create several objects while
  consuming only one unit of stock.

## Changes

- Adds server-readable quantity adjustment buttons and a selected-row state.
- Uses the shop session's real interaction anchor for range validation.
- Creates exactly the purchased stackable or non-stackable quantity.
- Decrements finite stock by the exact quantity and preserves unlimited stock.
- Clears per-player selection state when the shop session ends.

## Scope and application

- `scripts/merchant_shop_ui.lua`

```text
git apply --check merchant-purchasing.patch
git apply merchant-purchasing.patch
```

Restart after applying. Reverse with
`git apply -R merchant-purchasing.patch`.

## Validation

- Clean reverse-application check passed.
- Lua 5.1 syntax validation passed.
- Tested against LoA Eternal Dedicated Server game version `1.4.1.0`.

Because this file is client-window and purchase-path sensitive, verify finite,
unlimited, stackable, non-stackable, display-item, and animal purchases on a
test shard before production deployment.
