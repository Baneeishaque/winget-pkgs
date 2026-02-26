# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

The winget-pkgs repository is the official community-driven package repository for Microsoft's Windows Package Manager (winget). This codebase consists primarily of YAML manifest files organized in a hierarchical directory structure, where each package version is defined by multiple manifest files that specify installation details, localization data, and metadata. The repository follows strict naming conventions and supports extensive internationalization with manifests in multiple languages.

## Coding Conventions

### File Naming
- **Directory Structure**: `manifests/{first-letter}/{publisher}/{package}/{version}/`
- **Manifest Files**: PascalCase format `{Publisher}.{Package}.{type}.yaml`
- **Main Manifest**: `{Publisher}.{Package}.yaml`
- **Installer Manifest**: `{Publisher}.{Package}.installer.yaml`
- **Locale Manifests**: `{Publisher}.{Package}.locale.{language-code}.yaml`

### Manifest Types
```yaml
# Main manifest example
PackageIdentifier: Publisher.Package
PackageVersion: 1.0.0
DefaultLocale: en-US
ManifestType: version
ManifestVersion: 1.4.0

# Installer manifest example
PackageIdentifier: Publisher.Package
PackageVersion: 1.0.0
MinimumOSVersion: 10.0.0.0
ManifestType: installer
ManifestVersion: 1.4.0

# Locale manifest example
PackageIdentifier: Publisher.Package
PackageVersion: 1.0.0
PackageLocale: en-US
ManifestType: locale
ManifestVersion: 1.4.0
```

### Import/Export Patterns
- Mixed import styles for TypeScript components
- Mixed export patterns depending on module type
- No specific framework dependencies detected

## Workflows

### Add New Package Version
**Trigger:** When a software maintainer releases a new version of their application
**Command:** `/add-version`

1. Create version directory: `manifests/{first-letter}/{publisher}/{package}/{version}/`
2. Create installer manifest file: `{Publisher}.{Package}.installer.yaml`
   - Define installation methods, architecture support, and system requirements
3. Create English locale manifest: `{Publisher}.{Package}.locale.en-US.yaml`
   - Add package description, license, and English metadata
4. Create main package manifest: `{Publisher}.{Package}.yaml`
   - Reference version, default locale, and manifest metadata
5. Validate all manifest files follow schema requirements
6. Test package installation locally before submission

### Multi-Locale Package Support
**Trigger:** When adding a package version that supports Chinese, Norwegian, or other locales
**Command:** `/add-locales`

1. Complete standard package manifests (installer, en-US locale, main)
2. Create Chinese locale manifest: `{Publisher}.{Package}.locale.zh-CN.yaml`
   - Translate package name, description, and relevant metadata
3. Add additional locale manifests as needed:
   - Norwegian: `.locale.nb-NO.yaml`
   - Japanese: `.locale.ja-JP.yaml` 
   - Traditional Chinese: `.locale.zh-TW.yaml`
   - British English: `.locale.en-GB.yaml`
4. Ensure all locale manifests reference the same PackageIdentifier and PackageVersion
5. Verify translations are accurate and culturally appropriate

### JetBrains IDE EAP Updates
**Trigger:** When JetBrains releases new Early Access Program builds
**Command:** `/jetbrains-eap`

1. Create EAP version directory with build number: `manifests/j/JetBrains/{IDE}/EAP/{build}/`
2. Create EAP installer manifest: `{Publisher}.{Package}.EAP.installer.yaml`
   - Include EAP-specific download URLs and installation parameters
3. Add English locale manifest: `{Publisher}.{Package}.EAP.locale.en-US.yaml`
   - Mark as pre-release/EAP version in description
4. Add Chinese locale manifest: `{Publisher}.{Package}.EAP.locale.zh-CN.yaml`
5. Create main EAP manifest: `{Publisher}.{Package}.EAP.yaml`
6. Include appropriate pre-release tags and warnings

### DuckStudio Tools Comprehensive Update
**Trigger:** When DuckStudio releases new versions of FufuDevTools
**Command:** `/duck-studio-update`

1. Create version directory with date-based versioning pattern
2. Add installer manifest with updated download links
3. Create comprehensive locale support:
   - English (US): `.locale.en-US.yaml`
   - English (UK): `.locale.en-GB.yaml`
   - Japanese: `.locale.ja-JP.yaml`
   - Chinese (Simplified): `.locale.zh-CN.yaml`
   - Chinese (Traditional): `.locale.zh-TW.yaml`
4. Update main manifest with new version information
5. Verify all locale-specific information is properly translated

### Quick Package Updates
**Trigger:** When packages like DoltHub.Dolt or DifferentAI.OpenWork release frequent updates
**Command:** `/quick-update`

1. Create new version directory for incremental version number
2. Copy previous version manifests as templates
3. Update installer manifest:
   - New download URLs
   - Updated file hashes
   - Version-specific installation parameters
4. Update locale manifests with version-specific changes
5. Update main package manifest with new version reference
6. Perform quick validation against previous version

## Testing Patterns

- Test files follow `*.test.*` pattern
- Testing framework not clearly identified from analysis
- Manual validation through winget client recommended
- Schema validation for YAML manifests required
- Local installation testing before submission

## Commands

| Command | Purpose |
|---------|---------|
| `/add-version` | Add a new version of an existing package with standard manifests |
| `/add-locales` | Add comprehensive multi-language support to a package version |
| `/jetbrains-eap` | Handle JetBrains IDE Early Access Program releases |
| `/duck-studio-update` | Update DuckStudio tools with extensive locale support |
| `/quick-update` | Rapid updates for frequently released packages |