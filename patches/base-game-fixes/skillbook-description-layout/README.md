# Skillbook description layout

Provides a mod-safe override for the native skill detail page so expanded
descriptions are not silently ellipsized.

## Changes

- Loads the native skillbook with `require 'default:base_skill_window'`.
- Replaces only `AddSkillDetail`.
- Uses compact readable description text.
- Adds the full description as a tooltip fallback.
- Preserves skill icons, sliders, abilities, tracking, and favorites.

## Mod-only installation

This patch adds a new override file. Apply it at the root of a mod, not inside
the stock `aria` directory:

```text
git apply --check skillbook-description-layout.patch
git apply skillbook-description-layout.patch
```

The resulting path is `scripts/base_skill_window.lua`. Applying this additive
override directly to the base `aria` scripts would make the `default:` require
self-referential and is not supported.

Restart after installing the mod override. Remove the added file to roll back.

## Validation

- Clean reverse-application check passed.
- Lua 5.1 syntax validation passed.
- Tested against LoA Eternal Dedicated Server game version `1.4.1.0`.
