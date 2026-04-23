---
name: winget-pkgs-conventions
description: Development conventions and patterns for winget-pkgs. C# project with freeform commits.
---

# Winget Pkgs Conventions

> Generated from [Baneeishaque/winget-pkgs](https://github.com/Baneeishaque/winget-pkgs) on 2026-04-01

## Overview

This skill teaches Claude the development patterns and conventions used in winget-pkgs.

## Tech Stack

- **Primary Language**: C#
- **Architecture**: hybrid module organization
- **Test Location**: separate

## When to Use This Skill

Activate this skill when:
- Making changes to this repository
- Adding new features following established patterns
- Writing tests that match project conventions
- Creating commits with proper message format

## Commit Conventions

Follow these commit message conventions based on 200 analyzed commits.

### Commit Style: Free-form Messages

### Prefixes Used

- `feat`
- `update`

### Message Guidelines

- Average message length: ~58 characters
- Keep first line concise and descriptive
- Use imperative mood ("Add feature" not "Added feature")


*Commit message example*

```text
feat: add winget-pkgs ECC bundle (.claude/commands/remove-unsupported-package-version.md)
```

*Commit message example*

```text
Update: TandemHealth.Tandem version 2026.4.1 (2026.4.1-build43550+35deb30) (#354422)
```

*Commit message example*

```text
feat: add winget-pkgs ECC bundle (.claude/commands/update-existing-package-manifest.md)
```

*Commit message example*

```text
feat: add winget-pkgs ECC bundle (.claude/commands/add-new-package-version.md)
```

*Commit message example*

```text
feat: add winget-pkgs ECC bundle (.codex/agents/docs-researcher.toml)
```

*Commit message example*

```text
feat: add winget-pkgs ECC bundle (.codex/agents/reviewer.toml)
```

*Commit message example*

```text
feat: add winget-pkgs ECC bundle (.codex/agents/explorer.toml)
```

*Commit message example*

```text
feat: add winget-pkgs ECC bundle (.codex/AGENTS.md)
```

## Architecture

### Project Structure: Single Package

This project uses **hybrid** module organization.

### Guidelines

- This project uses a hybrid organization
- Follow existing patterns when adding new code

## Code Style

### Language: C#

### Naming Conventions

| Element | Convention |
|---------|------------|
| Files | PascalCase |
| Functions | camelCase |
| Classes | PascalCase |
| Constants | SCREAMING_SNAKE_CASE |

### Import Style: Relative Imports

### Export Style: Named Exports


*Preferred import style*

```typescript
// Use relative imports
import { Button } from '../components/Button'
import { useAuth } from './hooks/useAuth'
```

*Preferred export style*

```typescript
// Use named exports
export function calculateTotal() { ... }
export const TAX_RATE = 0.1
export interface Order { ... }
```

## Common Workflows

These workflows were detected from analyzing commit patterns.

### Feature Development

Standard feature implementation workflow

**Frequency**: ~8 times per month

**Steps**:
1. Add feature implementation
2. Add tests for feature
3. Update documentation

**Example commit sequence**:
```
feat: add winget-pkgs ECC bundle (.claude/ecc-tools.json)
feat: add winget-pkgs ECC bundle (.claude/skills/winget-pkgs/SKILL.md)
feat: add winget-pkgs ECC bundle (.agents/skills/winget-pkgs/SKILL.md)
```

### Add New Package Version

Adds a new version of a package to the winget-pkgs repository, including installer, main manifest, and locale files.

**Frequency**: ~20 times per month

**Steps**:
1. Create a new directory for the package version under manifests/<first-letter>/<Publisher>/<Package>/<Version>/
2. Add <Package>.installer.yaml
3. Add <Package>.yaml
4. Add one or more <Package>.locale.<locale>.yaml files (commonly en-US, zh-CN, etc.)

**Files typically involved**:
- `manifests/*/*/*/*/*.installer.yaml`
- `manifests/*/*/*/*/*.yaml`
- `manifests/*/*/*/*/*.locale.*.yaml`

**Example commit sequence**:
```
Create a new directory for the package version under manifests/<first-letter>/<Publisher>/<Package>/<Version>/
Add <Package>.installer.yaml
Add <Package>.yaml
Add one or more <Package>.locale.<locale>.yaml files (commonly en-US, zh-CN, etc.)
```

### Update Existing Package Manifest

Updates the manifest or installer file for an existing package version (e.g., URL or metadata changes).

**Frequency**: ~3 times per month

**Steps**:
1. Edit one or more manifest files for an existing package version under manifests/<first-letter>/<Publisher>/<Package>/<Version>/
2. Commit the changes

**Files typically involved**:
- `manifests/*/*/*/*/*.installer.yaml`
- `manifests/*/*/*/*/*.yaml`
- `manifests/*/*/*/*/*.locale.*.yaml`

**Example commit sequence**:
```
Edit one or more manifest files for an existing package version under manifests/<first-letter>/<Publisher>/<Package>/<Version>/
Commit the changes
```

### Remove Unsupported Package Version

Removes manifest files for a package version that is no longer supported.

**Frequency**: ~2 times per month

**Steps**:
1. Delete <Package>.installer.yaml, <Package>.yaml, and any <Package>.locale.*.yaml files for the unsupported version under manifests/<first-letter>/<Publisher>/<Package>/<Version>/
2. Commit the removal

**Files typically involved**:
- `manifests/*/*/*/*/*.installer.yaml`
- `manifests/*/*/*/*/*.yaml`
- `manifests/*/*/*/*/*.locale.*.yaml`

**Example commit sequence**:
```
Delete <Package>.installer.yaml, <Package>.yaml, and any <Package>.locale.*.yaml files for the unsupported version under manifests/<first-letter>/<Publisher>/<Package>/<Version>/
Commit the removal
```

### Add Ecc Bundle Command Or Agent

Adds a new ECC bundle command, agent, or configuration file for automation or documentation purposes.

**Frequency**: ~8 times per month

**Steps**:
1. Add a new markdown, yaml, toml, or json file under .claude/, .codex/, or .agents/ directories
2. Commit the new file

**Files typically involved**:
- `.claude/commands/*.md`
- `.claude/homunculus/instincts/inherited/*.yaml`
- `.codex/agents/*.toml`
- `.codex/AGENTS.md`
- `.codex/config.toml`
- `.claude/identity.json`
- `.agents/skills/winget-pkgs/**/*`
- `.claude/skills/winget-pkgs/**/*`
- `.claude/ecc-tools.json`

**Example commit sequence**:
```
Add a new markdown, yaml, toml, or json file under .claude/, .codex/, or .agents/ directories
Commit the new file
```


## Best Practices

Based on analysis of the codebase, follow these practices:

### Do

- Use PascalCase for file names
- Prefer named exports

### Don't

- Don't deviate from established patterns without discussion

---

*This skill was auto-generated by [ECC Tools](https://ecc.tools). Review and customize as needed for your team.*
