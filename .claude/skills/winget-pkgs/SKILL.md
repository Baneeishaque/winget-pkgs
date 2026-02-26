# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

The winget-pkgs repository is the community-driven package repository for Windows Package Manager (winget). This codebase primarily consists of YAML manifest files that define software packages, their versions, installers, and metadata. The repository follows a structured hierarchical organization with TypeScript tooling for validation and automation, though the core content is manifest-driven rather than code-driven.

## Coding Conventions

### File Naming
- **PascalCase** for all manifest files and directories
- Pattern: `{Publisher}.{Package}.{type}.yaml`
- Examples:
  - `Microsoft.VisualStudioCode.installer.yaml`
  - `Google.Chrome.locale.en-US.yaml`
  - `Adobe.Photoshop.yaml`

### Directory Structure
```
manifests/
├── {first-letter}/
│   └── {Publisher}/
│       └── {Package}/
│           └── {version}/
│               ├── {Publisher}.{Package}.yaml
│               ├── {Publisher}.{Package}.installer.yaml
│               ├── {Publisher}.{Package}.locale.en-US.yaml
│               └── {Publisher}.{Package}.locale.{country-code}.yaml
```

### Import/Export Style
- Mixed patterns detected in TypeScript tooling
- YAML manifests use structured key-value pairs
- Consistent indentation (2 spaces) in YAML files

## Workflows

### Remove Old Package Version
**Trigger:** When maintainers want to clean up old package versions that are no longer needed
**Command:** `/remove-version`

1. Navigate to the package version directory: `manifests/{letter}/{Publisher}/{Package}/{version}/`
2. Delete the installer manifest: `{Publisher}.{Package}.installer.yaml`
3. Delete the English locale manifest: `{Publisher}.{Package}.locale.en-US.yaml`
4. Delete any additional locale manifests (e.g., `{Publisher}.{Package}.locale.zh-CN.yaml`)
5. Delete the main package manifest: `{Publisher}.{Package}.yaml`
6. Remove the empty version directory
7. Commit with descriptive message about version removal

**Example:**
```bash
# Remove Microsoft Visual Studio Code version 1.74.0
rm -rf manifests/m/Microsoft/VisualStudioCode/1.74.0/
```

### Add New Package Version
**Trigger:** When a new version of a software package is released and needs to be added to winget
**Command:** `/new-version`

1. Create new version directory: `manifests/{letter}/{Publisher}/{Package}/{version}/`
2. Create installer manifest with download URLs and installation details:
   ```yaml
   # Microsoft.VisualStudioCode.installer.yaml
   PackageIdentifier: Microsoft.VisualStudioCode
   PackageVersion: 1.85.0
   InstallerType: inno
   Installers:
   - Architecture: x64
     InstallerUrl: https://update.code.visualstudio.com/1.85.0/win32-x64/stable
     InstallerSha256: [SHA256_HASH]
   ```
3. Create English locale manifest with descriptions and metadata:
   ```yaml
   # Microsoft.VisualStudioCode.locale.en-US.yaml
   PackageIdentifier: Microsoft.VisualStudioCode
   PackageVersion: 1.85.0
   PackageLocale: en-US
   Publisher: Microsoft Corporation
   ShortDescription: Code editor redefined and optimized for building modern web and cloud applications
   ```
4. Add additional locale manifests if the software supports multiple languages
5. Create main package manifest with version coordination:
   ```yaml
   # Microsoft.VisualStudioCode.yaml
   PackageIdentifier: Microsoft.VisualStudioCode
   PackageVersion: 1.85.0
   DefaultLocale: en-US
   ManifestType: version
   ManifestVersion: 1.4.0
   ```
6. Validate manifests using repository tooling
7. Commit with clear version addition message

### Update Package Installer
**Trigger:** When installer details need to be modified without changing other package metadata
**Command:** `/update-installer`

1. Locate the installer manifest: `manifests/{letter}/{Publisher}/{Package}/{version}/{Publisher}.{Package}.installer.yaml`
2. Update relevant fields such as:
   - InstallerUrl
   - InstallerSha256
   - InstallerSwitches
   - Dependencies
3. Validate the updated manifest
4. Commit with specific description of installer changes

**Example Update:**
```yaml
# Update installer switches
InstallerSwitches:
  Silent: /VERYSILENT /NORESTART
  SilentWithProgress: /SILENT /NORESTART
  Custom: /MERGETASKS=!runcode
```

## Testing Patterns

### Validation Framework
- Testing appears to use pattern matching on `*.test.*` files
- YAML manifest validation through automated pipelines
- Hash verification for installer URLs
- Schema validation against winget manifest specifications

### Common Test Scenarios
- Manifest syntax validation
- URL accessibility checks
- SHA256 hash verification
- Package identifier uniqueness
- Version format compliance

## Commands

| Command | Purpose |
|---------|---------|
| `/remove-version` | Remove an outdated package version and all associated manifests |
| `/new-version` | Add a complete new version of an existing package with all required manifests |
| `/update-installer` | Modify installer-specific details for an existing package version |
| `/validate-manifest` | Run validation checks on package manifests |
| `/check-hashes` | Verify SHA256 hashes for installer URLs |