```markdown
# winget-pkgs Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development and maintenance patterns used in the `winget-pkgs` repository, a C#-based project for managing Windows package manifests. You'll learn how to add, update, and remove package versions, as well as how to document project conventions and tooling. The guide covers coding conventions, workflow steps, and common commands to streamline contributions.

## Coding Conventions

- **File Naming:**  
  - Use PascalCase for C# files (e.g., `PackageManifest.cs`).
  - Manifest files follow the pattern:  
    - `<Package>.installer.yaml`  
    - `<Package>.locale.<locale>.yaml`  
    - `<Package>.yaml`

- **Import Style:**  
  - Use relative imports.  
    ```csharp
    using MyNamespace.Utilities;
    ```

- **Export Style:**  
  - Use named exports for classes and methods.  
    ```csharp
    public class PackageManifest
    {
        // ...
    }
    ```

- **Commit Messages:**  
  - Freeform style, often with prefixes like `feat` or `update`.
  - Example:  
    ```
    feat: add new version of Contoso.App 1.2.3
    update: fix installer URL for Fabrikam.Tool 2.0.1
    ```

## Workflows

### Add New Package Version
**Trigger:** When you want to add a new version of an existing package to the repository.  
**Command:** `/add-new-package-version`

1. Create a new directory under `manifests/<first-letter>/<Publisher>/<Package>/<Version>/`
2. Add the `<Package>.installer.yaml` file for the new version.
3. Add any required `<Package>.locale.<locale>.yaml` files (e.g., `en-US`, `zh-CN`).
4. Add the `<Package>.yaml` manifest file.
5. Commit your changes with a descriptive message.

**Example Directory Structure:**
```
manifests/C/Contoso/App/1.2.3/
  ├─ App.installer.yaml
  ├─ App.locale.en-US.yaml
  └─ App.yaml
```

### Update Existing Package Manifest
**Trigger:** When you need to update information (like URLs or installer details) for an existing package version.  
**Command:** `/update-existing-package-manifest`

1. Locate the existing manifest directory for the package version.
2. Edit one or more manifest files (usually `*.installer.yaml` or `*.locale.*.yaml`).
3. Commit the updated files with a clear message.

**Example:**
```yaml
# Edit App.installer.yaml to update the installer URL
InstallerUrl: https://new-url.com/installer.exe
```

### Remove Unsupported Package Version
**Trigger:** When a package version becomes unsupported and should be removed from the repository.  
**Command:** `/remove-package-version`

1. Locate the manifest directory for the unsupported package version.
2. Delete all related files: `*.installer.yaml`, `*.locale.*.yaml`, and `*.yaml`.
3. Commit the removal with an explanatory message.

**Example:**
```
git rm manifests/C/Contoso/App/1.1.0/*
```

### Add Conventions or Tooling Documentation
**Trigger:** When you want to document or configure project conventions, automation agents, or tooling.  
**Command:** `/add-convention-docs`

1. Create or update files in `.claude/`, `.codex/`, or `.agents/` directories.
2. Commit new or updated documentation, configuration, or agent definition files.

**Example:**
```
.claude/contributing.md
.codex/validation-rules.yaml
.agents/auto-reviewer.json
```

## Testing Patterns

- **Framework:** Unknown (not explicitly detected).
- **Test File Pattern:** Test files are named with the pattern `*.test.*`.
- **Example:**  
  ```
  PackageManifest.test.cs
  ```
- **Note:** Check for test files matching this pattern to understand or contribute tests.

## Commands

| Command                        | Purpose                                                        |
|--------------------------------|----------------------------------------------------------------|
| /add-new-package-version       | Add a new version of an existing package                       |
| /update-existing-package-manifest | Update manifest files for an existing package version           |
| /remove-package-version        | Remove manifest files for an unsupported package version        |
| /add-convention-docs           | Add or update documentation, configuration, or agent definitions|
```
