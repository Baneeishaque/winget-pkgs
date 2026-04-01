```markdown
# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches you how to contribute to the `winget-pkgs` repository, which manages package manifests for the Windows Package Manager (winget). You'll learn about the repository's coding conventions, how to add or update package manifests, and how to follow established workflows for maintaining package metadata.

## Coding Conventions

### File Naming
- **PascalCase** is used for file names.
  - Example: `MyPackage.yaml`, `MyPackage.installer.yaml`, `MyPackage.locale.en-US.yaml`

### Import Style
- **Relative imports** are used in C# files.
  - Example:
    ```csharp
    using MyNamespace.Models;
    ```

### Export Style
- **Named exports** are used.
  - Example:
    ```csharp
    public class PackageManifest { ... }
    ```

### Manifest File Structure
- Manifests are organized under:  
  `manifests/<first-letter>/<Publisher>/<Package>/<Version>/`
- Typical files per version:
  - `<Package>.yaml` (general metadata)
  - `<Package>.installer.yaml` (installer details)
  - `<Package>.locale.<lang>.yaml` (localized metadata)

## Workflows

### Add or Update Package Version
**Trigger:** When you want to add a new package or update an existing package to a new version.  
**Command:** `/add-or-update-package-version`

1. Create a new directory:  
   `manifests/<first-letter>/<Publisher>/<Package>/<Version>/`
2. Add `<Package>.installer.yaml` with installer metadata.
3. Add one or more `<Package>.locale.<lang>.yaml` files (e.g., `en-US`, `zh-CN`).
4. Add `<Package>.yaml` with general package metadata.

**Example directory structure:**
```
manifests/M/Microsoft/PowerToys/0.45.0/
  ├── PowerToys.yaml
  ├── PowerToys.installer.yaml
  ├── PowerToys.locale.en-US.yaml
```

### Update Single File Manifest
**Trigger:** When you need to update or fix a specific manifest file for a package version (e.g., installer or locale file).  
**Command:** `/update-single-file-manifest`

1. Edit the relevant file under:  
   `manifests/<first-letter>/<Publisher>/<Package>/<Version>/`
   - Usually `*.installer.yaml` or `*.locale.*.yaml`
2. Commit your change with a descriptive message.

**Example:**
- To update the English locale:
  - Edit `PowerToys.locale.en-US.yaml` in the relevant version directory.

### Revert Package Version
**Trigger:** When you need to undo a recent package version addition or update.  
**Command:** `/revert-package-version`

1. Restore or replace all manifest files for the affected version under:  
   `manifests/<first-letter>/<Publisher>/<Package>/<Version>/`
2. Ensure all files (`*.yaml`, `*.installer.yaml`, `*.locale.*.yaml`) are reverted to their previous state.

**Example:**
- To revert version `0.45.0` of PowerToys, restore all files in `manifests/M/Microsoft/PowerToys/0.45.0/` to their prior versions.

## Testing Patterns

- **Testing Framework:** Unknown (not detected in this analysis).
- **Test File Pattern:** Files matching `*.test.*`
  - Example: `PackageManifest.test.cs`
- Tests are likely written in C#, but the specific framework is not identified.

## Commands

| Command                        | Purpose                                                         |
|---------------------------------|-----------------------------------------------------------------|
| /add-or-update-package-version  | Add a new package or update an existing package version         |
| /update-single-file-manifest    | Update or fix a specific manifest file for a package version    |
| /revert-package-version         | Revert a previously added or updated package version            |
```