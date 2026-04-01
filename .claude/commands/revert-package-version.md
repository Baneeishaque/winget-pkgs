---
name: revert-package-version
description: Workflow command scaffold for revert-package-version in winget-pkgs.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /revert-package-version

Use this workflow when working on **revert-package-version** in `winget-pkgs`.

## Goal

Reverts a previously added or updated package version by restoring or replacing manifest files for that version.

## Common Files

- `manifests/*/*/*/*/*.installer.yaml`
- `manifests/*/*/*/*/*.locale.*.yaml`
- `manifests/*/*/*/*/*.yaml`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Restore or replace all manifest files for the affected version under manifests/<first-letter>/<Publisher>/<Package>/<Version>/

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.