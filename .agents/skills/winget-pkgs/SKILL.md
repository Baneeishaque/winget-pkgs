```markdown
# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches you how to contribute to the `winget-pkgs` repository, which manages package manifests for the Windows Package Manager (`winget`). You'll learn the repository's coding conventions, how to add, update, or remove package versions, and the commands and workflows used to maintain high-quality package metadata.

## Coding Conventions

### File Naming
- Use **PascalCase** for file names.
  - Example: `MyPackage.yaml`, `MyPackage.installer.yaml`, `MyPackage.locale.en-US.yaml`

### Import Style
- Use **relative imports** in C# files.
  - Example:
    ```csharp
    using MyNamespace.Utilities;
    ```

### Export Style
- Use **named exports**.
  - Example:
    ```csharp
    public class PackageManifest { ... }
    ```

### Commit Messages
- Freeform, but often start with `update`
- Keep messages concise (~57 characters on average)
  - Example: `update installer url for MyPackage 1.2.3`

## Workflows

### Add New Package Version
**Trigger:** When publishing a new version of a package  
**Command:** `/add-package-version`

1. Create a new directory:  
   `manifests/<first-letter>/<Publisher>/<Package>/<Version>/`
2. Add the installer metadata file:  
   `<Package>.installer.yaml`
3. Add locale files for supported languages:  
   `<Package>.locale.<locale>.yaml`
4. Add the main metadata file:  
   `<Package>.yaml`
5. Commit your changes with a descriptive message.

**Example Directory Structure:**
```
manifests/M/Microsoft/PowerToys/0.45.0/
  ├── PowerToys.yaml
  ├── PowerToys.installer.yaml
  └── PowerToys.locale.en-US.yaml
```

---

### Update Existing Package Manifest
**Trigger:** When updating metadata (e.g., installer URLs) for an existing package version  
**Command:** `/update-package-manifest`

1. Edit the relevant manifest files in the version directory:
   - `<Package>.installer.yaml`
   - `<Package>.locale.<locale>.yaml` (if needed)
2. Commit your changes with a message indicating the update.

**Example Commit Message:**
```
update installer url for PowerToys 0.45.0
```

---

### Remove Unsupported Package Version
**Trigger:** When deprecating or removing a package version  
**Command:** `/remove-package-version`

1. Delete the manifest files for the version:
   - `<Package>.installer.yaml`
   - `<Package>.locale.<locale>.yaml`
   - `<Package>.yaml`
2. Commit with a message indicating removal.

**Example Commit Message:**
```
remove PowerToys 0.45.0 manifests
```

## Testing Patterns

- **Testing Framework:** Unknown (not detected from analysis)
- **Test File Pattern:** Files containing `.test.` in their name (e.g., `ManifestParser.test.cs`)
- **Typical Usage:**  
  - Place test files alongside implementation files or in a dedicated test directory.
  - Use standard C# testing practices.

## Commands

| Command                | Purpose                                                      |
|------------------------|--------------------------------------------------------------|
| /add-package-version   | Add a new version of a package with all required manifests   |
| /update-package-manifest | Update installer URLs or metadata for an existing version   |
| /remove-package-version  | Remove all manifests for a deprecated or unsupported version|
```