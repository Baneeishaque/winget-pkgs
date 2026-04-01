```markdown
# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches you the core development and contribution patterns for the `winget-pkgs` repository, which is the central community-maintained source for Windows Package Manager (winget) manifests. The repository is primarily C#-based, but its main focus is on organizing, updating, and maintaining YAML manifest files that describe Windows software packages. You'll learn how to structure new package versions, follow coding conventions, and use common workflows for contributing to the repo.

## Coding Conventions

### File Naming
- **PascalCase** is used for file names.
  - Example: `MyPackage.yaml`, `MyPackage.installer.yaml`

### Import Style
- **Relative imports** are used in C# code.
  - Example:
    ```csharp
    using MyNamespace.Models;
    ```

### Export Style
- **Named exports** are used.
  - Example:
    ```csharp
    public class PackageManifest { ... }
    ```

### Commit Messages
- Freeform, but often start with `update`
- Average length: 58 characters
  - Example: `update MyPackage to version 2.1.0`

## Workflows

### Add or Update Package Version
**Trigger:** When you want to add a new version of an existing package or a new package to the Windows Package Manager (winget) repository.  
**Command:** `/add-package-version`

1. **Create a new directory** under `manifests/<first-letter>/<Publisher>/<PackageName>/<Version>/`
   - Example: `manifests/m/Microsoft/PowerToys/0.45.0/`
2. **Add the installer manifest**:  
   - `manifests/<first-letter>/<Publisher>/<PackageName>/<Version>/<PackageId>.installer.yaml`
   - Example: `PowerToys.installer.yaml`
3. **Add the English locale metadata**:  
   - `manifests/<first-letter>/<Publisher>/<PackageName>/<Version>/<PackageId>.locale.en-US.yaml`
   - Example: `PowerToys.locale.en-US.yaml`
4. **Optionally add additional locale files** (if the package supports multiple languages):  
   - `manifests/<first-letter>/<Publisher>/<PackageName>/<Version>/<PackageId>.locale.<other>.yaml`
   - Example: `PowerToys.locale.ja-JP.yaml`
5. **Add the general package metadata**:  
   - `manifests/<first-letter>/<Publisher>/<PackageName>/<Version>/<PackageId>.yaml`
   - Example: `PowerToys.yaml`

**Example Directory Structure:**
```
manifests/
  M/
    Microsoft/
      PowerToys/
        0.45.0/
          PowerToys.yaml
          PowerToys.installer.yaml
          PowerToys.locale.en-US.yaml
          PowerToys.locale.ja-JP.yaml
```

**Example Manifest File (`PowerToys.yaml`):**
```yaml
PackageIdentifier: Microsoft.PowerToys
PackageVersion: 0.45.0
Publisher: Microsoft
PackageName: PowerToys
...
```

## Testing Patterns

- **Framework:** Unknown (not detected)
- **Test File Pattern:** Files containing `.test.` in their names
  - Example: `PackageManifest.test.cs`
- **General Practice:** Place tests in files named with `.test.` to distinguish them from production code.

## Commands

| Command              | Purpose                                                        |
|----------------------|----------------------------------------------------------------|
| /add-package-version | Add or update a package version by creating the required YAML manifests and directory structure. |

```