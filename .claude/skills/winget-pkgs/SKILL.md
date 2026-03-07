# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the development patterns for the Windows Package Manager (winget) community repository. The winget-pkgs repository contains package manifests that define software packages available through the Windows Package Manager. Each package follows a structured YAML-based format with specific file naming conventions and directory structures organized alphabetically by publisher.

## Coding Conventions

### File Naming
- **Pattern**: PascalCase for all manifest files
- **Structure**: `{Publisher}.{Package}.{type}.yaml`
- **Examples**:
  ```
  Microsoft.VisualStudioCode.installer.yaml
  Microsoft.VisualStudioCode.locale.en-US.yaml
  Microsoft.VisualStudioCode.yaml
  ```

### Directory Structure
- **Pattern**: `manifests/{first-letter}/{publisher}/{package}/{version}/`
- **Example**: `manifests/m/Microsoft/VisualStudioCode/1.85.0/`

### Manifest Types
- **Main manifest**: `{Publisher}.{Package}.yaml` - Contains basic package information
- **Installer manifest**: `{Publisher}.{Package}.installer.yaml` - Download URLs and installation details  
- **Locale manifest**: `{Publisher}.{Package}.locale.{locale}.yaml` - Localized metadata and descriptions

## Workflows

### New Package Version
**Trigger:** When a software package releases a new version that needs to be made available through winget
**Command:** `/new-version`

1. Create the version directory: `manifests/{first-letter}/{publisher}/{package}/{version}/`
2. Create the installer manifest with download URLs and installation methods
3. Create the English locale manifest with package metadata and descriptions
4. Create the main manifest with basic package information
5. Add additional locale files if the package supports multiple languages

**Example structure:**
```
manifests/m/Microsoft/VisualStudioCode/1.85.0/
├── Microsoft.VisualStudioCode.installer.yaml
├── Microsoft.VisualStudioCode.locale.en-US.yaml
└── Microsoft.VisualStudioCode.yaml
```

### New Package Creation
**Trigger:** When a new software application needs to be added to winget for the first time
**Command:** `/new-package`

1. Create the publisher directory structure if it doesn't exist
2. Create the package directory under the publisher
3. Create the initial version directory
4. Create installer manifest with download URLs and install methods
5. Create locale manifest with comprehensive package metadata
6. Create main manifest with basic package information

### Mozilla Thunderbird Localized Version
**Trigger:** When Mozilla releases a new Thunderbird version that needs to be available in multiple languages
**Command:** `/thunderbird-locale`

1. Create installer manifest for the specific locale version
2. Create English locale manifest (en-US) with base metadata
3. Create localized manifest (e.g., zh-CN) with translated descriptions
4. Create main manifest with version and locale information

**Example structure:**
```
manifests/m/Mozilla/Thunderbird/ESR/zh-CN/115.6.0/
├── Mozilla.Thunderbird.ESR.zh-CN.installer.yaml
├── Mozilla.Thunderbird.ESR.zh-CN.locale.en-US.yaml
├── Mozilla.Thunderbird.ESR.zh-CN.locale.zh-CN.yaml
└── Mozilla.Thunderbird.ESR.zh-CN.yaml
```

### Mozilla Firefox Localized Version
**Trigger:** When Mozilla releases a new Firefox version that needs extensive multi-language support
**Command:** `/firefox-locale`

1. Create installer manifest for the specific locale version
2. Create multiple locale manifest files for different languages
3. Create main manifest with basic package information
4. Ensure proper locale codes are used in file names

### Speakeasy CLI Version
**Trigger:** When the Speakeasy CLI tool releases a new version via automated release process
**Command:** `/speakeasy-version`

1. Create installer manifest with new CLI version and download URLs
2. Create English locale manifest with updated metadata
3. Create main manifest with version information
4. Typically automated through bot processes

### Package Removal
**Trigger:** When a package version needs to be removed due to issues, vulnerabilities, or other concerns
**Command:** `/remove-package`

1. Remove the installer manifest file
2. Remove all locale manifest files
3. Remove the main manifest file
4. Remove the version directory if it becomes empty
5. Document the reason for removal in commit message

## Testing Patterns

The repository uses automated validation through GitHub Actions to ensure:
- YAML syntax is valid
- Manifest schema compliance
- Download URL accessibility
- Hash verification for installers

Test files follow the pattern `*.test.*` though specific testing framework details are not clearly defined in the current analysis.

## Commands

| Command | Purpose |
|---------|---------|
| `/new-version` | Add a new version of an existing package (~40+/day) |
| `/new-package` | Create a brand new package entry (~5/day) |
| `/thunderbird-locale` | Add localized Mozilla Thunderbird version (~10/day) |
| `/firefox-locale` | Add localized Mozilla Firefox version (~2/day) |
| `/speakeasy-version` | Update Speakeasy CLI tool version (~3/day) |
| `/remove-package` | Remove a specific package version (~1/day) |