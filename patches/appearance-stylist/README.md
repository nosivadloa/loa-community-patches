# Appearance stylist NPC

Adds a generic NPC that opens the native character appearance editor for
players.

## Features

- Talk-based stylist window with interaction-range enforcement.
- Uses the stock `custom_char_window` editor.
- Prevents appearance changes during an active conflict.
- Freezes the player while editing.
- Requires confirmation before retaining the new appearance.
- Provides a ready-to-spawn, invulnerable stylist template.

## Scope

- `scripts/community_appearance_stylist.lua`
- `scripts/community_appearance_service.lua`
- `templates/mobiles/community_appearance_stylist.xml`

The names are deliberately generic and the service is complimentary. Shards
can add currency charging, different clothing, or custom dialogue after
applying the package.

## Apply

From a mod root containing, or intended to contain, `scripts` and `templates`:

```text
git apply --check appearance-stylist.patch
git apply appearance-stylist.patch
```

Restart the server, then spawn `community_appearance_stylist` using the shard's
normal template-spawning workflow. Reverse with:

```text
git apply -R appearance-stylist.patch
```

## Verification checklist

1. Spawn the stylist and use its Talk interaction.
2. Open the appearance editor and commit a change.
3. Reject a proposed change and reopen the editor.
4. Confirm the editor is blocked during an active conflict.
5. Restart while editing and confirm the service recovers safely.

## Validation

- Applies cleanly to an empty mod root.
- Both Lua files pass Lua 5.1 syntax validation.
- The mobile template parses as XML.
- Contains no shard-specific runtime dependency or branding.
