# Vendor bank-gold payments

Allows gold-based vendor purchases to draw from a player's backpack, bank, or
both balances together.

This is an optional economy and convenience change. Stock behavior already
supports bank fallback in some legacy purchase paths, but coverage and balance
handling are inconsistent across vendor windows.

## What changes

- NPC merchant cart windows display backpack plus bank gold as spendable.
- Player-hired vendor windows display the same combined spendable balance.
- Legacy single-item vendor confirmation dialogs use the same payment plan.
- A purchase uses the backpack when it covers the bill, otherwise the bank
  when it covers the bill, otherwise a split payment.
- Split payments debit the backpack first and the remaining amount from the
  bank.
- If the bank stage fails, the backpack debit is refunded.
- Successful bank-funded purchases report the amount paid from the bank.

## Scope

- `scripts/merchant_shop_ui.lua`
- `scripts/player_vendor_shop_ui.lua`
- `scripts/base_transaction.lua`

## Compatibility and dependency

The `merchant_shop_ui.lua` hunk is generated on top of the repository's
[`Merchant purchasing repair`](../../base-game-fixes/merchant-purchasing/).
Apply that base-game fix first. Do not also apply the narrower Merchant
quantity-selection patch because those two base fixes overlap.

The patch contains full transaction-state changes. If another mod overrides
any scoped file, merge the hunks instead of replacing that file.

## Apply

From the directory containing `scripts`, after applying Merchant purchasing
repair:

```text
git apply --check vendor-bank-gold-payments.patch
git apply vendor-bank-gold-payments.patch
```

Restart the server after applying. Reverse with:

```text
git apply -R vendor-bank-gold-payments.patch
```

## Verification checklist

1. Buy from an NPC merchant using backpack gold only.
2. Buy from an NPC merchant using bank gold only.
3. Buy with neither balance sufficient alone but the combined balance sufficient.
4. Repeat the three cases at a player-hired vendor.
5. Complete a bank-funded purchase through a legacy single-item dialog.
6. Confirm an insufficient combined balance consumes no gold.
7. Simulate a failed second-stage bank debit and confirm backpack gold is refunded.

## Validation

- Confirmed working on the Nosivad Planars test server.
- Lua 5.1 syntax validation passed for all three scripts.
- Payment-model tests passed for backpack-only, bank-only, split,
  insufficient-funds, and failed-bank-stage rollback cases.
- Source-invariant validation passed.
- Production launcher and runtime copies were SHA-256 verified after deployment.
