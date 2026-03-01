```markdown
# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

The winget-pkgs repository is the official Microsoft Windows Package Manager (winget) community repository containing software package manifests. This repository follows a structured YAML-based approach for defining software packages, their versions, and metadata. The codebase is primarily focused on package manifest management with a hierarchical directory structure organized by publisher and package names.

## Coding Conventions

### File Naming
- **Directory Structure**: `manifests/{letter}/{publisher}/{package}/{version}/`
- **Manifest Files**: Use PascalCase with specific suffixes:
  - `{Publisher}.{Package}.yaml` - Main package manifest
  - `{Publisher}.{Package}.installer.yaml` - Installer-specific manifest
  - `{Publisher}.{Package}.locale.en-US.yaml` - English localization
  - `{Publisher}.{Package}.locale.{lang}.yaml` - Additional localizations

### Manifest Structure
- All manifests use YAML format with strict schema validation
- Version numbers follow semantic versioning where possible
- Package identifiers use Publisher.PackageName format

### Commit Patterns
- Use descriptive prefixes: `modify`, `update`
- Keep commit messages concise (average 58 characters)
- Focus on the specific package or change being made

## Workflows

### Add New Package Version
**Trigger:** When a software package releases a new version
**Command:** `/new-version`

1. Navigate to the package directory: `manifests/{letter}/{publisher}/{package}/`
2. Create new version directory with exact version number
3. Generate the installer manifest (`.installer.yaml`) with:
   - Package version
   - Download URLs and architectures
   - Installation parameters
   - File hashes and signatures
4. Create locale manifest (`.locale.en-US.yaml`) with:
   - Package description
   - Release notes
   - Tags and categories
5. Generate main package manifest (`.yaml`) with:
   - Package identifier
   - Version reference
   - Manifest version
6. Add additional locale files for internationalized packages
7. Validate all manifests against schema

### Remove Package Version
**Trigger:** When a package version needs to be removed due to issues or cleanup
**Command:** `/remove-version`

1. Identify the target version directory
2. Remove the installer manifest (`.installer.yaml`)
3. Remove the locale manifest (`.locale.en-US.yaml`)
4. Remove the main package manifest (`.yaml`)
5. Delete any additional locale files
6. Remove the empty version directory
7. Verify no references to the removed version exist

### Fix Package Manifest
**Trigger:** When package metadata needs correction or updating
**Command:** `/fix-manifest`

1. Identify the problematic manifest file (usually installer.yaml)
2. Locate the specific issue (incorrect URL, hash, or metadata)
3. Update the affected fields while maintaining schema compliance
4. Verify the fix doesn't break existing functionality
5. Test manifest validation
6. Commit with descriptive message indicating the fix

### Update Package Metadata
**Trigger:** When package metadata needs updating for existing version
**Command:** `/update-metadata`

1. Navigate to the target version directory
2. Update installer manifest if installation details changed
3. Modify locale-specific manifests for:
   - Updated descriptions
   - New release notes
   - Additional tags or categories
4. Maintain the same version number
5. Validate all updated manifests
6. Ensure consistency across all locale files

### Add New Package
**Trigger:** When a new software package is being added for the first time
**Command:** `/add-package`

1. Determine the correct directory structure based on publisher name
2. Create publisher directory if it doesn't exist
3. Create package directory under the publisher
4. Create the first version directory (usually latest stable version)
5. Generate complete installer manifest with all supported architectures
6. Create comprehensive locale manifest with full package information
7. Generate main package manifest with proper identifiers
8. Set up additional localization files if package supports multiple languages
9. Validate entire package structure
10. Test installation flow if possible

## Testing Patterns

### Manifest Validation
- All manifests must pass schema validation
- Use automated tools to verify YAML syntax and structure
- Test files follow `*.test.*` pattern
- Validation includes hash verification and URL accessibility

### Integration Testing
- Package installation testing on clean Windows systems
- Multi-architecture compatibility verification
- Locale-specific functionality testing

## Commands

| Command | Purpose |
|---------|---------|
| `/new-version` | Add a new version of an existing software package |
| `/remove-version` | Remove an existing version from the repository |
| `/fix-manifest` | Fix or update specific manifest files |
| `/update-metadata` | Update package information without version change |
| `/add-package` | Add a completely new software package |
| `/validate` | Run schema validation on manifest files |
| `/check-urls` | Verify all download URLs are accessible |
```