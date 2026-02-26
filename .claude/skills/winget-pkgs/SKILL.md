# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

The winget-pkgs repository is Microsoft's Windows Package Manager community repository containing package manifests for software distribution. This codebase follows a highly structured YAML-based manifest system where packages are organized by vendor and version, with specific conventions for package metadata, installers, and localization.

## Coding Conventions

### File Structure
- **Directory naming**: `manifests/{first-letter}/{vendor}/{package}/{version}/`
- **Manifest naming**: PascalCase format following `{Vendor}.{Package}.{type}.yaml`
- **File types**: 
  - Main manifest: `{Vendor}.{Package}.yaml`
  - Installer manifest: `{Vendor}.{Package}.installer.yaml` 
  - Locale manifests: `{Vendor}.{Package}.locale.{locale}.yaml`

### Commit Patterns
- **Style**: Freeform with descriptive messages
- **Common prefixes**: `update`, `add`, `remove`
- **Length**: Average 58 characters
- **Example**: `update Microsoft.VisualStudioCode to version 1.85.0`

### YAML Conventions
- Use consistent indentation (2 spaces)
- Follow winget manifest schema specifications
- Include required fields: PackageIdentifier, PackageVersion, DefaultLocale
- Maintain alphabetical ordering where applicable

## Workflows

### New Package Version Release
**Trigger:** When a software maintainer releases a new version of their application
**Command:** `/new-version`

1. Create version-specific directory under `manifests/{letter}/{vendor}/{package}/{version}/`
2. Add installer manifest with download URLs, checksums, and installation parameters
3. Add English locale manifest with package description and metadata
4. Add main package manifest linking all components
5. Optionally add additional locale manifests for internationalization

**Example structure:**
```
manifests/m/Microsoft/VisualStudioCode/1.85.0/
├── Microsoft.VisualStudioCode.installer.yaml
├── Microsoft.VisualStudioCode.locale.en-US.yaml
└── Microsoft.VisualStudioCode.yaml
```

### New Package Creation
**Trigger:** When adding a new software application that has never been in winget before
**Command:** `/new-package`

1. Create complete package directory structure from scratch
2. Add installer manifest with architecture-specific installers
3. Add English locale manifest with comprehensive package information
4. Add main package manifest establishing the package identity
5. Validate manifest schema compliance

### Package Version Removal
**Trigger:** When a package version needs to be removed due to issues or cleanup
**Command:** `/remove-version`

1. Remove installer manifest file
2. Remove all associated locale manifest files
3. Remove main package manifest file
4. Clean up version directory (should be empty after manifest removal)
5. Verify no broken references remain

### Package Metadata Update
**Trigger:** When package information needs to be corrected or enhanced
**Command:** `/update-metadata`

1. Modify installer manifest for installation parameter changes
2. Update locale manifests for description or metadata corrections
3. Maintain version consistency across all manifest files
4. Validate updated manifests against schema

### Multi-Locale Firefox Release
**Trigger:** When Mozilla releases a new Firefox Developer Edition build for multiple language variants
**Command:** `/firefox-multi-locale`

1. Create version directory for each locale variant
2. Add installer manifest for each locale with appropriate download URLs
3. Add English and Chinese locale manifests as needed
4. Add main package manifest for each locale variant
5. Coordinate release timing across all locale packages

### Elastic Stack Synchronized Release
**Trigger:** When Elastic releases a new version of their monitoring stack tools
**Command:** `/elastic-stack-release`

1. Update each Elastic component (Elasticsearch, Kibana, Logstash, etc.)
2. Add installer and locale manifests for each component
3. Ensure version consistency across all Elastic stack components
4. Coordinate simultaneous release of all components

## Testing Patterns

Testing appears to be handled through automated validation systems rather than traditional unit tests. The repository likely uses:
- YAML schema validation for manifest structure
- Automated installer testing through CI/CD pipelines
- Package installation verification on Windows systems

## Commands

| Command | Purpose |
|---------|---------|
| `/new-version` | Add a new version of an existing package |
| `/new-package` | Create a completely new package entry |
| `/remove-version` | Remove a specific package version |
| `/update-metadata` | Update existing package metadata |
| `/firefox-multi-locale` | Handle coordinated Firefox releases |
| `/elastic-stack-release` | Manage synchronized Elastic stack updates |