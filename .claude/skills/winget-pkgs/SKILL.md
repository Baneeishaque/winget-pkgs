# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

The winget-pkgs repository is the community-driven package manifest repository for Microsoft's Windows Package Manager (winget). This repository contains package manifests written in YAML format that define how software packages are installed, updated, and managed on Windows systems. The codebase follows a structured directory layout with packages organized by publisher and version, supporting multiple locales and installation architectures.

## Coding Conventions

### File Naming
- **Directory Structure**: PascalCase for publisher and package names
- **Manifest Files**: Follow pattern `{Publisher}.{Package}.{type}.yaml`
- **Locale Files**: Use standard locale codes (en-US, zh-CN, ja-JP)

### YAML Structure
```yaml
# Example installer manifest
PackageIdentifier: Microsoft.VisualStudioCode
PackageVersion: 1.74.0
InstallerLocale: en-US
Platform:
- Windows.Desktop
InstallerType: inno
Scope: user
InstallModes:
- interactive
- silent
- silentWithProgress
```

### Directory Organization
```
manifests/
├── m/
│   └── Microsoft/
│       └── VisualStudioCode/
│           └── 1.74.0/
│               ├── Microsoft.VisualStudioCode.installer.yaml
│               ├── Microsoft.VisualStudioCode.locale.en-US.yaml
│               ├── Microsoft.VisualStudioCode.locale.zh-CN.yaml
│               └── Microsoft.VisualStudioCode.yaml
```

## Workflows

### New Package Version Release
**Trigger:** When a software package releases a new version
**Command:** `/new-version`

1. Create new version directory under `manifests/{first-letter}/{publisher}/{package}/{version}/`
2. Generate `{Publisher}.{Package}.installer.yaml` with:
   - Download URLs and checksums
   - Installation parameters
   - Architecture support
   - Silent install switches
3. Create `{Publisher}.{Package}.locale.en-US.yaml` with:
   - Package description and summary
   - Publisher information
   - License details
   - Documentation URLs
4. Generate main `{Publisher}.{Package}.yaml` with:
   - Package identifier
   - Version number
   - Manifest version
5. Validate all YAML files for syntax and completeness

**Example commit message:** `New version: Microsoft.VisualStudioCode version 1.74.0`

### Multilingual Package Support
**Trigger:** When releasing software packages that target international markets
**Command:** `/add-locales`

1. Create standard English locale file (`locale.en-US.yaml`)
2. Add Chinese locale support:
   ```yaml
   # Microsoft.Package.locale.zh-CN.yaml
   PackageLocale: zh-CN
   Publisher: 发布者名称
   PackageName: 软件包名称
   ShortDescription: 简短描述
   Description: 详细描述
   ```
3. Optionally add Japanese locale:
   ```yaml
   # Microsoft.Package.locale.ja-JP.yaml
   PackageLocale: ja-JP
   Publisher: パブリッシャー
   PackageName: パッケージ名
   ```
4. Ensure all locale files reference the same PackageIdentifier and PackageVersion

### Package Manifest Maintenance
**Trigger:** When package metadata needs correction or enhancement
**Command:** `/fix-manifest`

1. Identify the specific manifest component requiring updates:
   - **Installer issues**: Update `installer.yaml`
   - **Metadata problems**: Modify `locale.en-US.yaml`
   - **Version conflicts**: Check main `package.yaml`
2. Common fixes include:
   - Correcting download URLs or checksums
   - Updating package descriptions or publisher info
   - Fixing installation parameters
   - Adding missing dependencies or requirements
3. Test changes locally if possible
4. Submit with descriptive commit message

**Example commit message:** `Microsoft.VisualStudioCode: Update installer architecture support`

### Package Version Removal
**Trigger:** When a package version needs to be removed due to issues or policy violations
**Command:** `/remove-version`

1. Remove `{Publisher}.{Package}.installer.yaml`
2. Remove `{Publisher}.{Package}.locale.en-US.yaml`
3. Remove any additional locale files (`locale.zh-CN.yaml`, `locale.ja-JP.yaml`)
4. Remove main `{Publisher}.{Package}.yaml`
5. Clean up empty version directory
6. Document reason for removal in commit message

**Example commit message:** `Remove version: Publisher.Package version 1.0.0 (security vulnerability)`

## Testing Patterns

### Manifest Validation
- YAML syntax validation for all manifest files
- Schema validation against winget manifest specifications
- Cross-reference validation between related manifest files
- URL accessibility checks for download links
- Checksum verification for installer files

### Test File Pattern
- Test files follow `*.test.*` naming convention
- Automated validation runs on pull requests
- Community review process for package additions

## Commands

| Command | Purpose |
|---------|---------|
| `/new-version` | Add a new version of an existing package with complete manifest set |
| `/add-locales` | Add multilingual support (Chinese, Japanese) to existing packages |
| `/fix-manifest` | Update or correct existing package manifest metadata |
| `/remove-version` | Remove a specific package version from the repository |
| `/validate-yaml` | Check YAML syntax and schema compliance for manifests |