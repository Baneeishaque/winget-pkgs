---
name: update-existing-package-manifest
description: Workflow command scaffold for update-existing-package-manifest in winget-pkgs.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /update-existing-package-manifest

Use this workflow when working on **update-existing-package-manifest** in `winget-pkgs`.

## Goal

Updates the manifest files of an existing package version, such as updating URLs or metadata.

## Common Files

- `manifests/*/*/*/*/*.installer.yaml`
- `manifests/*/*/*/*/*.locale.*.yaml`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Locate the existing manifest directory for the package version
- Edit one or more manifest files (usually *.installer.yaml or *.locale.*.yaml)
- Commit the updated files

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.