---
name: remove-unsupported-package-version
description: Workflow command scaffold for remove-unsupported-package-version in winget-pkgs.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /remove-unsupported-package-version

Use this workflow when working on **remove-unsupported-package-version** in `winget-pkgs`.

## Goal

Removes manifest files for a package version that is no longer supported.

## Common Files

- `manifests/*/*/*/*/*/*.installer.yaml`
- `manifests/*/*/*/*/*/*.locale.*.yaml`
- `manifests/*/*/*/*/*/*.yaml`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Delete <Package>.installer.yaml and related locale and main yaml files from the version directory
- Commit with a message indicating removal

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.