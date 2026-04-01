---
name: update-single-file-manifest
description: Workflow command scaffold for update-single-file-manifest in winget-pkgs.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /update-single-file-manifest

Use this workflow when working on **update-single-file-manifest** in `winget-pkgs`.

## Goal

Updates a single manifest file for a package version, typically for minor changes or corrections (e.g., installer or locale file).

## Common Files

- `manifests/*/*/*/*/*.installer.yaml`
- `manifests/*/*/*/*/*.locale.*.yaml`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit a single file under manifests/<first-letter>/<Publisher>/<Package>/<Version>/, usually *.installer.yaml or *.locale.*.yaml

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.