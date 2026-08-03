# Contributing

Contributions should be small enough to review and test independently.

## Patch layout

Create one directory per fix:

```text
patches/<short-patch-name>/
  README.md
  <short-patch-name>.patch
```

The patch README should document:

1. Observable symptoms.
2. Root cause.
3. Files and behavior changed.
4. Application and rollback instructions.
5. LoA/server version or stock-file hash used for validation.
6. Tests performed and any known limitations.

## Patch requirements

- Use unified diff format with repository-relative paths.
- Do not include full upstream game files or proprietary assets.
- Avoid unrelated formatting changes.
- Run `git apply --check` against a clean stock copy.
- Validate Lua changes with a compatible Lua parser when possible.
- Explain any persistent-data migration or server restart requirement.
- Never include passwords, access tokens, webhook URLs, player data, or server
  credentials.

## Pull requests

Use a concise title and explain the player impact, root cause, and validation.
One logical fix per pull request keeps review and rollback straightforward.
