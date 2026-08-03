# Merchant quantity selection

Adds server-readable quantity controls to merchant buy windows and makes
checkout deliver and consume the exact selected quantity.

## Why this patch exists

Object-bound dynamic windows do not reliably submit the stock quantity text
field to the server. Players can therefore see a quantity field without being
able to use it consistently.

The base non-stackable purchase path also consumes only one stock unit even
when asked to deliver a larger quantity.

## Changes

- Clicking a normal row's Buy button selects and highlights that row.
- The footer provides `-10`, `-1`, `+1`, `+10`, and `Max` controls.
- Quantity is clamped between 1 and the available stock count.
- Sale animals retain the stock single-item purchase behavior.
- Stackable purchases create one stack with the selected amount.
- Non-stackable purchases create the selected number of individual objects.
- Finite stock is reduced by the exact delivered quantity.
- Unlimited stock remains unlimited.
- Per-player row-selection state is cleared when the shop closes.

## Scope

- `scripts/merchant_shop_ui.lua`

This is the quantity-only alternative to the broader
[`merchant-purchasing`](../merchant-purchasing/) patch. Do not apply both;
their quantity hunks intentionally overlap. The broader patch additionally
changes interaction-range handling for display-item and animal shop anchors.

## Apply

From the directory containing `scripts`:

```text
git apply --check merchant-quantity-selection.patch
git apply merchant-quantity-selection.patch
```

Restart the server after applying. Reverse with:

```text
git apply -R merchant-quantity-selection.patch
```

## Verification checklist

On a test shard, buy:

1. A finite stackable item at quantities 1, 2, 10, and Max.
2. An unlimited stackable item.
3. A finite non-stackable item at quantities 2 and 10.
4. An unlimited non-stackable item.
5. A sale animal, confirming it remains single-item.

## Validation

- Applies cleanly to untouched LoA Eternal Dedicated Server `1.4.1.0` stock.
- Lua 5.1 syntax validation passed.
- The generated diff contains no interaction-range changes.
