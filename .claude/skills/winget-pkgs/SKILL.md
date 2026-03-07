# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

The winget-pkgs repository is the official community repository for Windows Package Manager (winget) manifests. It contains structured YAML manifest files that define how packages are installed, configured, and presented to users through the winget command-line tool. The repository follows a strict hierarchical structure with vendor/package/version organization and supports multi-locale, multi-architecture package definitions.

## Coding Conventions

### File Structure
- **Manifest Organization**: `manifests/{vendor}/{package}/{version}/`
- **File Naming**: PascalCase with vendor prefix (e.g., `Mozilla.Firefox.installer.yaml`)
- **Directory Structure**: Hierarchical vendor → package → version pattern

### Manifest Types
```yaml
# Root manifest: {Package}.yaml
PackageIdentifier: Vendor.Package
PackageVersion: 1.0.0
DefaultLocale: en-US
ManifestType: version
ManifestVersion: 1.0.0

# Installer manifest: {Package}.installer.yaml
PackageIdentifier: Vendor.Package
PackageVersion: 1.0.0
Installers:
- Architecture: x64
  InstallerUrl: https://example.com/installer.exe
  InstallerSha256: [hash]
ManifestType: installer

# Locale manifest: {Package}.locale.{lang}.yaml
PackageIdentifier: Vendor.Package
PackageVersion: 1.0.0
PackageLocale: en-US
Publisher: Vendor Name
PackageName: Package Name
ManifestType: locale
```

### Import/Export Patterns
- Mixed import/export styles due to YAML structure
- Consistent YAML formatting with proper indentation
- Standard manifest type declarations

## Workflows

### New Package Version Release
**Trigger:** When a package maintainer releases a new version of their software
**Command:** `/new-version`

1. Create new version directory under `manifests/{vendor}/{package}/{version}/`
2. Generate installer manifest with download URLs and SHA256 hashes
3. Create locale manifest(s) with updated package metadata and descriptions
4. Add root manifest with version information and manifest references
5. Validate all YAML files follow the manifest schema
6. Submit pull request with descriptive commit message

**Example Structure:**
```
manifests/m/Microsoft/VisualStudioCode/1.85.0/
├── Microsoft.VisualStudioCode.installer.yaml
├── Microsoft.VisualStudioCode.locale.en-US.yaml
└── Microsoft.VisualStudioCode.yaml
```

### Mozilla Firefox ESR Localized Release
**Trigger:** When Mozilla releases a new Firefox ESR version that needs to be distributed in multiple languages
**Command:** `/firefox-esr-release`

1. Create version directory for each locale variant (e.g., `de-DE`, `en-US`, `zh-CN`)
2. Add installer manifest for each locale-specific build with appropriate download URLs
3. Generate multiple locale manifests supporting different languages
4. Create root manifest for each locale variant
5. Ensure consistent version numbering across all locale variants
6. Validate locale-specific metadata and descriptions

**Example Structure:**
```
manifests/m/Mozilla/Firefox/ESR/de-DE/115.6.0/
├── Mozilla.Firefox.ESR.de-DE.installer.yaml
├── Mozilla.Firefox.ESR.de-DE.locale.de-DE.yaml
├── Mozilla.Firefox.ESR.de-DE.locale.en-US.yaml
└── Mozilla.Firefox.ESR.de-DE.yaml
```

### Multi-Locale Package Release
**Trigger:** When releasing software that has built-in internationalization support
**Command:** `/multi-locale-release`

1. Create unified version directory structure
2. Add installer manifest with multi-architecture support (x86, x64, ARM64)
3. Generate locale manifests for each supported language
4. Create root manifest with default locale specification
5. Ensure consistent package metadata across all locales
6. Test installer URLs and validate SHA256 hashes

**Example Installer Manifest:**
```yaml
Installers:
- Architecture: x64
  InstallerUrl: https://example.com/app-x64.msi
  InstallerSha256: [hash]
- Architecture: x86
  InstallerUrl: https://example.com/app-x86.msi
  InstallerSha256: [hash]
```

### Single File Package Update
**Trigger:** When fixing package metadata, release notes, or installer configuration
**Command:** `/fix-package`

1. Identify the specific manifest file requiring modification
2. Update relevant metadata, URLs, or configuration parameters
3. Validate changes against manifest schema
4. Ensure version consistency across related manifest files
5. Create focused commit with clear description of changes

### Package Version Removal
**Trigger:** When a package version needs to be withdrawn due to security issues or other problems
**Command:** `/remove-version`

1. Remove installer manifest from version directory
2. Delete all associated locale manifests
3. Remove root manifest file
4. Clean up empty version directory structure
5. Document removal reason in commit message
6. Notify relevant stakeholders of package withdrawal

## Testing Patterns

### Validation Framework
- **Schema Validation**: All YAML files must conform to winget manifest schema
- **URL Testing**: Installer URLs must be accessible and return expected content
- **Hash Verification**: SHA256 hashes must match downloaded installer files
- **Locale Testing**: Multi-locale packages require validation across all supported languages

### Test File Patterns
- Files matching `*.test.*` pattern for automated validation
- Continuous integration runs schema validation on all pull requests
- Automated testing of installer download links and hash verification

## Commands

| Command | Purpose |
|---------|---------|
| `/new-version` | Add a new version of an existing package |
| `/firefox-esr-release` | Handle Mozilla Firefox ESR multi-locale release |
| `/multi-locale-release` | Release package with multiple language support |
| `/fix-package` | Update or fix existing package metadata |
| `/remove-version` | Remove problematic package version from repository |
| `/validate-manifest` | Validate YAML manifest against schema |
| `/check-urls` | Verify installer download URLs and hashes |
| `/update-locale` | Update locale-specific package information |