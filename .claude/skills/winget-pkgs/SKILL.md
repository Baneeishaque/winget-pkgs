# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill covers development patterns for the winget-pkgs repository, Microsoft's community-driven package manifest repository for Windows Package Manager. The codebase consists primarily of YAML manifest files organized in a structured directory hierarchy, with TypeScript tooling for validation and automation. Contributors maintain package definitions through standardized YAML schemas following strict naming and organizational conventions.

## Coding Conventions

### File Naming
- **Directory Structure**: Uses alphabetical organization `manifests/{first-letter}/{Publisher}/{Package}/{version}/`
- **File Names**: Follow PascalCase pattern: `{Publisher}.{Package}.{type}.yaml`
- **Manifest Types**: 
  - Main: `Publisher.Package.yaml`
  - Installer: `Publisher.Package.installer.yaml` 
  - Locale: `Publisher.Package.locale.{locale-code}.yaml`

### YAML Structure
```yaml
# Main manifest example
PackageIdentifier: Publisher.Package
PackageVersion: 1.0.0
DefaultLocale: en-US
ManifestType: version
ManifestVersion: 1.4.0
```

### Import/Export Patterns
- Mixed import styles detected in TypeScript tooling
- Manifest files reference each other through PackageIdentifier consistency
- Version dependencies managed through ManifestVersion field

### Commit Conventions
- **Style**: Freeform with common prefixes
- **Common Prefixes**: `update`, `modify`
- **Average Length**: 58 characters
- **Pattern**: Brief, descriptive messages focusing on package/version changes

## Workflows

### New Package Version
**Trigger:** When a software maintainer releases a new version of their application
**Command:** `/new-version`

1. Create the version directory: `manifests/{letter}/{Publisher}/{Package}/{version}/`
2. Generate installer YAML with download URLs and SHA256 hashes:
```yaml
PackageIdentifier: Publisher.Package
PackageVersion: 1.0.0
InstallerUrls:
  - Architecture: x64
    InstallerUrl: https://example.com/installer.exe
    InstallerSha256: [SHA256_HASH]
ManifestType: installer
ManifestVersion: 1.4.0
```
3. Create/update locale YAML with metadata and descriptions:
```yaml
PackageIdentifier: Publisher.Package
PackageVersion: 1.0.0
PackageLocale: en-US
Publisher: Publisher Name
PackageName: Package Name
ShortDescription: Brief description
ManifestType: defaultLocale
ManifestVersion: 1.4.0
```
4. Create main package YAML linking version and dependencies
5. Validate all three files maintain consistent PackageIdentifier and PackageVersion

### Mozilla Firefox Dev Update
**Trigger:** When Mozilla releases a new Firefox Developer Edition build
**Command:** `/update-firefox-dev`

1. Identify all Firefox Developer Edition locale variants in the repository
2. Update installer.yaml for each locale variant simultaneously:
```yaml
PackageIdentifier: Mozilla.Firefox.DeveloperEdition.locale
PackageVersion: 125.0b1
Installers:
  - InstallerUrl: https://ftp.mozilla.org/pub/firefox/releases/125.0b1/win64/{locale}/
    InstallerSha256: [NEW_HASH]
```
3. Maintain identical version numbers across all locale variants
4. Update download URLs and SHA256 hashes per locale-specific installer
5. Commit all locale updates in a single batch operation

### Add Package Tags
**Trigger:** When improving package discoverability or categorization
**Command:** `/add-tags`

1. Navigate to the target package's locale file: `{Publisher}.{Package}.locale.en-US.yaml`
2. Add or modify the Tags section:
```yaml
Tags:
  - developer
  - ide
  - programming
  - code-editor
```
3. Ensure tags are relevant and follow repository tagging conventions
4. Update without modifying PackageVersion (metadata-only change)
5. Validate YAML syntax and schema compliance

### Package Removal/Revert
**Trigger:** When a package version needs to be withdrawn due to issues
**Command:** `/remove-version`

1. Identify all manifest files for the target version:
   - `{Publisher}.{Package}.yaml`
   - `{Publisher}.{Package}.installer.yaml`
   - `{Publisher}.{Package}.locale.en-US.yaml`
   - Any additional locale files
2. Remove all files simultaneously to maintain consistency
3. Check if version directory becomes empty and remove if so
4. Verify no broken references remain in related manifests
5. Document removal reason in commit message

### Multilingual Package
**Trigger:** When publishing packages with international language support
**Command:** `/new-multilingual`

1. Create standard installer and main YAML files
2. Create primary English locale file:
```yaml
PackageIdentifier: Publisher.Package
PackageVersion: 1.0.0
PackageLocale: en-US
Publisher: Publisher Name
# ... English metadata
ManifestType: defaultLocale
```
3. Add additional locale files (e.g., zh-CN, de-DE):
```yaml
PackageIdentifier: Publisher.Package
PackageVersion: 1.0.0
PackageLocale: zh-CN
Publisher: 发布者名称
PackageName: 软件包名称
# ... Localized metadata
ManifestType: locale
```
4. Ensure consistent PackageIdentifier and PackageVersion across all locales
5. Validate all locale files against schema requirements

## Testing Patterns

### Validation Framework
- Test files follow `*.test.*` pattern
- Unknown testing framework detected (likely custom YAML validation)
- Schema validation against ManifestVersion specifications
- URL accessibility and hash verification for installer links

### Quality Checks
- YAML syntax validation
- Required field presence verification
- PackageIdentifier consistency across manifest types
- SHA256 hash accuracy for installer downloads

## Commands

| Command | Purpose |
|---------|---------|
| `/new-version` | Add a new version of an existing package with all required manifest files |
| `/update-firefox-dev` | Batch update Mozilla Firefox Developer Edition across all locales |
| `/add-tags` | Add or modify metadata tags in package locale files |
| `/remove-version` | Remove or revert a package version and all associated manifest files |
| `/new-multilingual` | Create a new package with multiple language locale support |