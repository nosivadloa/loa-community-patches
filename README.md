# Legends of Aria Community Patches

Small, reviewable fixes for Legends of Aria server developers and shard
operators.

Each patch lives in its own folder under [`patches/`](patches/) and includes:

- a unified diff that can be reviewed before application;
- installation and compatibility notes;
- the root cause and player/developer impact;
- the validation performed by the contributor.

## Available patches

The repository currently contains eight independently documented patches for
achievements, professions, Barding, merchants, skill/stat scaling, and the
skillbook UI. See the [patch index](patches/) for descriptions and links.

## Applying a patch

Read the patch-specific documentation first. From the directory containing the
target `scripts` folder, the usual workflow is:

```text
git apply --check path/to/fix.patch
git apply path/to/fix.patch
```

If your server files are not under version control, make a backup before
applying a patch. Restart or reload the affected scripts as directed by the
patch documentation.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Keep patches focused, explain the root
cause, and include reproducible validation.

## Disclaimer

This is an independent community project and is not an official Legends of
Aria distribution. Test every patch on a non-production shard before deploying
it to players.

## License

Repository documentation and original patch contributions are available under
the [MIT License](LICENSE). Upstream game files remain subject to their
respective owners' terms; this repository distributes diffs rather than full
upstream source files.
