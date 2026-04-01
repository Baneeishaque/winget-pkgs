---
name: add-new-package-version
description: Workflow command scaffold for add-new-package-version in winget-pkgs.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-new-package-version

Use this workflow when working on **add-new-package-version** in `winget-pkgs`.

## Goal

Adds a new version of an existing package to the winget-pkgs repository by creating a new manifest directory with installer, locale, and main yaml files.

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

- Create a new directory under manifests/<first-letter>/<Publisher>/<Package>/<Version>/
- Add <Package>.installer.yaml with installer metadata
- Add one or more <Package>.locale.<locale>.yaml files for supported languages
- Add <Package>.yaml with general package metadata

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.