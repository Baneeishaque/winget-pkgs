# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the development patterns for the winget-pkgs repository, Microsoft's community-driven package manifest repository for the Windows Package Manager (winget). The codebase consists primarily of YAML manifest files organized in a hierarchical directory structure, with TypeScript tooling for validation and automation. Package manifests are structured into installer, main package, and locale-specific files to support multi-language software distribution.

## Coding Conventions

### File Naming
- **Directory Structure**: PascalCase throughout the hierarchy
- **Manifest Files**: Follow the pattern `{Publisher}.{Package}.{Type}.yaml`
- **Path Structure**: `manifests/{first-letter}/{Publisher}/{Package}/{Version}/`

### File Types
```yaml
# Main package manifest
Publisher.Package.yaml

# Installer-specific manifest  
Publisher.Package.installer.yaml

# Locale-specific manifests
Publisher.Package.locale.en-US.yaml
Publisher.Package.locale.zh-CN.yaml
```

### Import/Export Style
- Mixed import and export patterns used across TypeScript tooling
- YAML manifests follow winget schema specifications
- Consistent indentation and structure within manifest files

## Workflows

### Add New Package Version
**Trigger:** When a new version of an existing software package is released
**Command:** `/new-package-version`

1. Create a new version directory under `manifests/{first-letter}/{Publisher}/{Package}/{Version}/`
2. Generate the installer manifest file (`{Publisher}.{Package}.installer.yaml`) with:
   - Download URLs and file hashes
   - Installation parameters and requirements
   - Architecture and platform specifications
3. Create the main package manifest (`{Publisher}.{Package}.yaml`) containing:
   - Package metadata and version information
   - Dependency references
4. Add the English locale manifest (`{Publisher}.{Package}.locale.en-US.yaml`) with:
   - Display names and descriptions
   - Publisher information and licensing details
5. Optionally add additional locale manifests for international support

**Example structure:**
```
manifests/m/Microsoft/VisualStudioCode/1.85.0/
├── Microsoft.VisualStudioCode.installer.yaml
├── Microsoft.VisualStudioCode.yaml
├── Microsoft.VisualStudioCode.locale.en-US.yaml
└── Microsoft.VisualStudioCode.locale.zh-CN.yaml
```

### Update Package Installer
**Trigger:** When installer details change for an existing package version without creating a new version
**Command:** `/update-installer`

1. Locate the existing installer manifest file in the appropriate version directory
2. Update the installer-specific metadata such as:
   - Download URLs if mirrors change
   - File hashes if installers are republished
   - Installation switches or parameters
   - Architecture support changes

**Common updates:**
```yaml
# Update installer URLs
Installers:
- Architecture: x64
  InstallerUrl: https://new-cdn.example.com/installer.exe
  InstallerSha256: NEW_SHA256_HASH_HERE
```

### Add Multilingual Package
**Trigger:** When adding software packages that have official multi-language support
**Command:** `/new-multilingual-package`

1. Create the standard package directory structure
2. Generate installer and main package manifests following standard patterns
3. Create the primary English locale manifest (`locale.en-US.yaml`)
4. Add Chinese locale support (`locale.zh-CN.yaml`) with translated:
   - Package names and descriptions
   - Publisher information
   - License and copyright details
5. Add additional locales (it-IT, ja-JP, etc.) as needed for the software

**Locale manifest example:**
```yaml
# locale.zh-CN.yaml
PackageLocale: zh-CN
Publisher: 发布商名称
PackageDescription: 软件包的中文描述
```

## Testing Patterns

- Test files follow the `*.test.*` pattern
- Testing framework not definitively detected from analysis
- Validation likely occurs through:
  - YAML schema validation
  - Manifest completeness checks
  - URL and hash verification
  - Multi-locale consistency validation

## Commands

| Command | Purpose |
|---------|---------|
| `/new-package-version` | Add a new version of an existing package with all required manifests |
| `/update-installer` | Update installer-specific details for an existing package version |
| `/new-multilingual-package` | Create a new package with multiple language locale support |