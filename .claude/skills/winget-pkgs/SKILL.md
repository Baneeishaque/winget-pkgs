# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the development patterns for contributing to the winget-pkgs repository, which contains package manifests for the Windows Package Manager (winget). The repository uses YAML manifest files organized in a structured directory hierarchy to define software packages, their versions, installers, and metadata. Contributors typically add new package versions or update existing package information through well-defined manifest structures.

## Coding Conventions

### File Naming
- **Pattern:** PascalCase for all manifest files
- **Structure:** `{Publisher}.{Package}.{type}.yaml`
- **Examples:**
  ```
  Microsoft.VisualStudioCode.installer.yaml
  Microsoft.VisualStudioCode.locale.en-US.yaml
  Microsoft.VisualStudioCode.yaml
  ```

### Directory Structure
- **Pattern:** `manifests/{first-letter}/{publisher}/{package}/{version}/`
- **Example:** `manifests/m/Microsoft/VisualStudioCode/1.85.0/`

### Import/Export Style
- Mixed patterns used across the codebase
- Follows YAML manifest specifications for winget

### Commit Conventions
- **Style:** Freeform with common prefixes
- **Common prefixes:** `modify`, `update`
- **Average length:** 58 characters
- **Examples:**
  ```
  update Microsoft.VisualStudioCode to 1.85.0
  modify installer hash for Adobe.Photoshop
  ```

## Workflows

### New Package Version
**Trigger:** When a software package releases a new version that needs to be added to Windows Package Manager
**Command:** `/new-version`

1. Create the version directory structure: `manifests/{letter}/{publisher}/{package}/{version}/`
2. Create installer manifest (`{publisher}.{package}.installer.yaml`) with:
   - Download URLs for each architecture
   - SHA256 checksums
   - Installation parameters
   - Dependencies
3. Create locale manifest (`{publisher}.{package}.locale.en-US.yaml`) with:
   - Package descriptions
   - Author information
   - License details
   - Tags and categories
4. Create main package manifest (`{publisher}.{package}.yaml`) with:
   - Package identifier
   - Version number
   - Manifest version
5. Optionally add additional locale manifests for other languages

**Example structure:**
```yaml
# Microsoft.VisualStudioCode.installer.yaml
PackageIdentifier: Microsoft.VisualStudioCode
PackageVersion: 1.85.0
Installers:
- Architecture: x64
  InstallerType: inno
  InstallerUrl: https://az764295.vo.msecnd.net/stable/.../VSCodeSetup-x64-1.85.0.exe
  InstallerSha256: ABC123...
```

### Update Package Installer
**Trigger:** When package installer details need to be updated (new hash, URL change, etc.) without changing version
**Command:** `/update-installer`

1. Locate the existing installer manifest file
2. Update the relevant fields:
   - InstallerUrl (if changed)
   - InstallerSha256 (always verify)
   - Installation parameters (if needed)
3. Commit with descriptive message about what was updated

### KDE Package Update
**Trigger:** When KDE software gets new nightly or development builds
**Command:** `/kde-update`

1. Navigate to the KDE package directory: `manifests/k/KDE/{package}/{version}/`
2. Update the installer manifest with:
   - New build number
   - Updated SHA256 hash
   - Verify installer URL is current
3. Commit with build number reference

**Example:**
```yaml
# KDE.Kdenlive.installer.yaml update
InstallerUrl: https://binary-factory.kde.org/.../kdenlive-21.12.3-1457-windows-msvc2019_64-cl.exe
InstallerSha256: DEF456...
```

## Testing Patterns

### Test Framework
- Framework: Unknown/Custom validation
- File pattern: `*.test.*`
- Validation likely occurs through:
  - YAML schema validation
  - URL accessibility checks
  - Hash verification
  - Manifest completeness validation

### Validation Process
1. Schema validation against winget manifest specifications
2. URL reachability tests for installer downloads
3. SHA256 hash verification
4. Required field completeness checks

## Commands

| Command | Purpose |
|---------|---------|
| `/new-version` | Add a complete new version of a software package with all required manifests |
| `/update-installer` | Update only the installer manifest of an existing package version |
| `/kde-update` | Update KDE software packages with new build numbers and hashes |
| `/validate-manifest` | Check manifest files for schema compliance and required fields |
| `/check-hash` | Verify SHA256 checksums for installer files |