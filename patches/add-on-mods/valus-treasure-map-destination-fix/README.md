# Exclude Valus from treasure-map destinations

Removes the town-center `Area-Valus` region from the stock treasure-map and
SOS-map destination pools.

## Why this package exists

Some shards do not have a valid or desirable treasure placement area inside
the Valus town region. Leaving it in the random destination pool can produce a
map target that cannot be completed reliably.

## Changes

- Removes only `{"Area-Valus","Valus"}` from five SOS-map tiers and two
  treasure-map tiers.
- Leaves West Valusia, East Valusia, and every other regional destination
  unchanged.

## Scope

- `templates/items/sos_map.xml` through `sos_map_4.xml`
- `templates/items/treasure_map.xml`
- `templates/items/treasure_map_1.xml`

This is a shard-layout compatibility patch, not a universal requirement. Apply
it only if `Area-Valus` is unsuitable for treasure placement on your map.

## Apply

From the directory containing `templates`:

```text
git apply --check valus-treasure-map-destination-fix.patch
git apply valus-treasure-map-destination-fix.patch
```

Restart the server after applying. Reverse with:

```text
git apply -R valus-treasure-map-destination-fix.patch
```

## Verification checklist

1. Generate each SOS-map tier repeatedly and confirm none selects Valus.
2. Generate both treasure-map tiers repeatedly with the same check.
3. Confirm East and West Valusia remain eligible.

## Validation

- Applies cleanly to untouched LoA Eternal Dedicated Server `1.4.1.0` stock.
- All seven modified templates parse as XML.
- The diff removes only the seven `Area-Valus` destination entries.
