# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

The winget-pkgs repository is Microsoft's community-driven package repository for the Windows Package Manager (winget). This codebase primarily consists of YAML manifest files that define package metadata, installation instructions, and localization data. The repository follows a structured directory layout where packages are organized by publisher and version, with each package version containing multiple YAML files for different aspects of the package definition.

## Coding Conventions

### File Naming
- **PascalCase** for all file names: `Microsoft.VisualStudioCode.yaml`
- Manifest files follow the pattern: `{Publisher}.{Package}.{Type}.yaml`
- Types include: main manifest (`.yaml`), installer (`.installer.yaml`), locale (`.locale.{lang}.yaml`)

### Directory Structure
```
manifests/
├── {first-letter}/
│   └── {Publisher}/
│       └── {Package}/
│           └── {Version}/
│               ├── {Publisher}.{Package}.yaml
│               ├── {Publisher}.{Package}.installer.yaml
│               └── {Publisher}.{Package}.locale.{language}.yaml
```

### YAML Structure
- Use consistent indentation (2 spaces)
- Follow semantic versioning for PackageVersion
- Include required fields: PackageIdentifier, PackageVersion, DefaultLocale, ManifestType, ManifestVersion

### Commit Messages
- Average length: 58 characters
- Common prefixes: "update", "add", "remove"
- Format: `update Microsoft.VisualStudioCode to 1.85.0`

## Workflows

### New Package Version Basic
**Trigger:** When someone wants to publish a new version of a package to winget  
**Command:** `/add-package-version`

1. Create the version directory under `manifests/{first-letter}/{publisher}/{package}/{version}/`
2. Create `{package}.installer.yaml` with download URLs, checksums, and installation instructions
3. Create `{package}.locale.en-US.yaml` with English package metadata (name, description, license, etc.)
4. Create main `{package}.yaml` file linking the installer and locale manifests
5. Validate all YAML syntax and required fields
6. Submit pull request with descriptive commit message

**Example files:**
- `Microsoft.VisualStudioCode.installer.yaml`
- `Microsoft.VisualStudioCode.locale.en-US.yaml` 
- `Microsoft.VisualStudioCode.yaml`

### New Package Version Multilingual
**Trigger:** When someone wants to publish a new version of a package with international language support  
**Command:** `/add-package-version-i18n`

1. Create the version directory structure
2. Create `{package}.installer.yaml` with download URLs and installation instructions
3. Create multiple locale files for different languages:
   - `{package}.locale.en-US.yaml` (required default)
   - `{package}.locale.de-DE.yaml`
   - `{package}.locale.zh-CN.yaml`
   - Additional languages as needed
4. Create main `{package}.yaml` file with DefaultLocale set to en-US
5. Ensure all locale files contain translated metadata
6. Validate and submit pull request

### Firefox ESR Localized Release
**Trigger:** When Mozilla releases a new Firefox ESR version for different language markets  
**Command:** `/firefox-esr-release`

1. For each language variant (de, zh-CN, etc.):
   - Create directory: `manifests/m/Mozilla/Firefox/ESR/{lang}/{version}/`
   - Create `Mozilla.Firefox.ESR.{lang}.installer.yaml` with language-specific installer
   - Create multiple locale files: `Mozilla.Firefox.ESR.{lang}.locale.{language}.yaml`
   - Create main manifest: `Mozilla.Firefox.ESR.{lang}.yaml`
2. Ensure installer URLs point to correct language-specific downloads
3. Include proper language tags in PackageLocale
4. Batch commit all language variants together

### Package Update
**Trigger:** When someone needs to fix or update package information for an existing version  
**Command:** `/update-package`

1. Locate existing package files in `manifests/{path}/{version}/`
2. Modify `{package}.installer.yaml` if updating:
   - Download URLs
   - File checksums
   - Installation parameters
   - Dependencies
3. Update locale files if changing:
   - Package descriptions
   - Publisher information
   - License details
4. Increment ManifestVersion if making significant changes
5. Test changes and submit focused pull request

### Package Removal
**Trigger:** When a package version needs to be withdrawn due to issues or policy violations  
**Command:** `/remove-package-version`

1. Identify the complete set of files for the version:
   - Main manifest file
   - Installer manifest file
   - All locale manifest files
2. Delete entire version directory: `manifests/{path}/{version}/`
3. Verify no other packages depend on this version
4. Create pull request with clear explanation for removal
5. Follow up on any dependent packages that may need updates

## Testing Patterns

The repository uses automated validation through GitHub Actions to ensure:
- YAML syntax correctness
- Required fields presence
- Manifest schema compliance
- File naming conventions
- Directory structure adherence

Test files follow the pattern `*.test.*` though the specific testing framework is not clearly identified from the repository structure.

## Commands

| Command | Purpose |
|---------|---------|
| `/add-package-version` | Create a new package version with basic English localization |
| `/add-package-version-i18n` | Create a new package version with multiple language support |
| `/firefox-esr-release` | Handle Mozilla Firefox ESR multi-language release process |
| `/update-package` | Modify existing package metadata or installer information |
| `/remove-package-version` | Remove a specific package version from the repository |