# Merchant stock-transform safety

Adds complete position and rotation transforms to affected Carpenter, Scribe,
and General Store stock entries in Eldeir, Helm, Pyros, and Valus.

## Symptoms and root cause

Some stock entries omit complete transform data. The base merchant restoration
path can fail while deserializing those entries, leaving a saved merchant
partly initialized or unable to open its shop.

## Scope

The patch updates 12 stock merchant templates under `templates/celador/`.
It does not change player inventory or pricing.

## Apply

```text
git apply --check merchant-stock-transform-safety.patch
git apply merchant-stock-transform-safety.patch
```

Restart after applying.

## Existing saved merchants

This patch prevents the malformed template data from being loaded again, but
it does not automatically replace already damaged saved-world merchant
objects. Back up the world database and use your shard's normal object repair
or template-respawn workflow for affected existing merchants.

## Rollback and validation

Reverse with `git apply -R merchant-stock-transform-safety.patch`. All 12
patched templates pass XML parsing. Tested against LoA Eternal Dedicated
Server game version `1.4.1.0`.
