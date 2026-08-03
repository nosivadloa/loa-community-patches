# Patch index

Packages are separated by intent so operators can distinguish corrections to
stock behavior from optional features and shard-rule changes.

## Base-game fixes

These packages correct broken, incomplete, or inconsistent behavior in the
stock LoA Eternal server while preserving the intended feature.

| Patch | Purpose |
| --- | --- |
| [Barding and Provoke repair](base-game-fixes/barding-provoke/) | Corrects visible-skill progression, two-target flow, difficulty, threat, and cooldown behavior. |
| [Merchant purchasing repair](base-game-fixes/merchant-purchasing/) | Fixes quantity selection, shop-anchor range checks, and exact stock consumption. |
| [Merchant quantity selection](base-game-fixes/merchant-quantity-selection/) | Adds reliable quantity controls and exact stackable/non-stackable checkout without changing interaction range. |
| [Merchant stock-transform safety](base-game-fixes/merchant-stock-transform-safety/) | Completes malformed merchant stock transforms that can break saved shops. |
| [Profession progression repair](base-game-fixes/profession-progression/) | Enables authored later tiers and repairs trainer/objective data across active professions. |
| [Profession-rank enforcement](base-game-fixes/profession-rank-enforcement/) | Enforces earned combat-profession ranks for books, training, hotbar actions, and use. |
| [Configurable secondary-stat scaling](base-game-fixes/secondary-stat-scaling/) | Scales Wisdom/Will gain eligibility from configured skill and stat caps. |
| [Shared achievement-type claim fix](base-game-fixes/shared-achievement-type-fix/) | Fixes unclaimable shared-type achievement rewards and missing Magery icons. |
| [Skillbook description layout](base-game-fixes/skillbook-description-layout/) | Adds a mod-safe detail renderer with full-description tooltip fallback. |

## Add-on mods

These packages intentionally enable an optional feature, change a shard rule,
or add new content. Review their gameplay and economy impact before deployment.

| Mod | Purpose |
| --- | --- |
| [Appearance stylist NPC](add-on-mods/appearance-stylist/) | Adds a generic NPC that safely opens the native character appearance editor. |
| [Expanded skill-cap compatibility](add-on-mods/expanded-skill-cap-compatibility/) | Supports quest notifications and controlled spawn pacing when total skill caps exceed 600. |
| [Enable marketplace boards](add-on-mods/marketplace-boards-enable/) | Removes the stock guard that disables township marketplace-board functionality. |
| [Unrestricted sewer teleporter](add-on-mods/unrestricted-sewer-teleporter/) | Removes the legacy profession-selection gate from sewer teleporters. |
| [Valus treasure-map destination exclusion](add-on-mods/valus-treasure-map-destination-fix/) | Excludes an unsuitable Valus town region from stock treasure and SOS map pools. |
| [Vendor bank-gold payments](add-on-mods/vendor-bank-gold-payments/) | Allows NPC and player-vendor purchases to use backpack gold, bank gold, or both balances together. |
