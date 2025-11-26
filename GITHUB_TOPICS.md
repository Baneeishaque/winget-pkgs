# GitHub Topics and Tags for winget-pkgs Repository

This document provides recommended GitHub topics and tags for the Windows Package Manager Community Repository, along with various methods to add them.

## Recommended GitHub Topics

Based on the analysis of this repository, the following topics are recommended:

### Core Topics (Essential)
| Topic | Description |
|-------|-------------|
| `winget` | The Windows Package Manager this repository supports |
| `winget-pkgs` | Identifies this as the WinGet packages repository |
| `windows-package-manager` | Full descriptive name of the package manager |
| `package-manager` | General category for package management |
| `windows` | Target operating system |
| `microsoft` | Original creator/maintainer |

### Technical Topics
| Topic | Description |
|-------|-------------|
| `yaml` | Manifest file format used in this repository |
| `manifest` | Repository contains software package manifests |
| `packages` | Contains software package definitions |
| `software-distribution` | Purpose of the repository |

### Ecosystem/Format Topics
| Topic | Description |
|-------|-------------|
| `winget-cli` | Related Windows Package Manager CLI tool |
| `windows-installer` | Related to Windows application installation |
| `msix` | Supported installer format |
| `msi` | Supported installer format |
| `appx` | Supported installer format |

### Community Topics
| Topic | Description |
|-------|-------------|
| `hacktoberfest` | Indicates participation in Hacktoberfest events |
| `open-source` | Open source nature of the repository |
| `community` | Community-driven contributions |
| `package-repository` | Type of repository |

---

## Methods to Add GitHub Topics

### Method 1: GitHub CLI (gh)

The GitHub CLI provides the easiest command-line way to manage repository topics.

#### Prerequisites
```bash
# Install GitHub CLI (if not already installed)
# On Windows (winget):
winget install GitHub.cli

# On macOS:
brew install gh

# On Linux (Debian/Ubuntu):
sudo apt install gh
```

#### Authenticate with GitHub
```bash
gh auth login
```

#### Add Topics Using GitHub CLI

**Set all topics at once (replaces existing topics):**
```bash
gh repo edit Baneeishaque/winget-pkgs --add-topic "winget,winget-pkgs,windows-package-manager,package-manager,windows,microsoft,yaml,manifest,packages,software-distribution,winget-cli,windows-installer,msix,msi,appx,hacktoberfest,open-source,community,package-repository"
```

**Add individual topics:**
```bash
gh repo edit Baneeishaque/winget-pkgs --add-topic winget
gh repo edit Baneeishaque/winget-pkgs --add-topic winget-pkgs
gh repo edit Baneeishaque/winget-pkgs --add-topic windows-package-manager
gh repo edit Baneeishaque/winget-pkgs --add-topic package-manager
gh repo edit Baneeishaque/winget-pkgs --add-topic windows
gh repo edit Baneeishaque/winget-pkgs --add-topic microsoft
gh repo edit Baneeishaque/winget-pkgs --add-topic yaml
gh repo edit Baneeishaque/winget-pkgs --add-topic manifest
gh repo edit Baneeishaque/winget-pkgs --add-topic packages
gh repo edit Baneeishaque/winget-pkgs --add-topic software-distribution
gh repo edit Baneeishaque/winget-pkgs --add-topic winget-cli
gh repo edit Baneeishaque/winget-pkgs --add-topic windows-installer
gh repo edit Baneeishaque/winget-pkgs --add-topic msix
gh repo edit Baneeishaque/winget-pkgs --add-topic msi
gh repo edit Baneeishaque/winget-pkgs --add-topic appx
gh repo edit Baneeishaque/winget-pkgs --add-topic hacktoberfest
gh repo edit Baneeishaque/winget-pkgs --add-topic open-source
gh repo edit Baneeishaque/winget-pkgs --add-topic community
gh repo edit Baneeishaque/winget-pkgs --add-topic package-repository
```

**Remove a topic:**
```bash
gh repo edit Baneeishaque/winget-pkgs --remove-topic <topic-name>
```

**View current topics:**
```bash
gh repo view Baneeishaque/winget-pkgs --json repositoryTopics
```

---

### Method 2: GitHub REST API

You can use the GitHub REST API directly with curl or any HTTP client.

#### Using curl

**Get current topics:**
```bash
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer YOUR_GITHUB_TOKEN" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/Baneeishaque/winget-pkgs/topics
```

**Replace all topics:**
```bash
curl -L \
  -X PUT \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer YOUR_GITHUB_TOKEN" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/Baneeishaque/winget-pkgs/topics \
  -d '{"names":["winget","winget-pkgs","windows-package-manager","package-manager","windows","microsoft","yaml","manifest","packages","software-distribution","winget-cli","windows-installer","msix","msi","appx","hacktoberfest","open-source","community","package-repository"]}'
```

---

### Method 3: GitHub Web Interface

1. Navigate to your repository: https://github.com/Baneeishaque/winget-pkgs
2. Click on the ⚙️ **gear icon** next to "About" on the right sidebar
3. In the "Topics" field, enter topics separated by spaces or commas
4. Click **Save changes**

#### Recommended topics to copy-paste:
```
winget winget-pkgs windows-package-manager package-manager windows microsoft yaml manifest packages software-distribution winget-cli windows-installer msix msi appx hacktoberfest open-source community package-repository
```

---

### Method 4: GitHub GraphQL API

For more advanced use cases, you can use the GraphQL API.

#### Query to get repository ID:
```graphql
query {
  repository(owner: "Baneeishaque", name: "winget-pkgs") {
    id
    repositoryTopics(first: 20) {
      nodes {
        topic {
          name
        }
      }
    }
  }
}
```

#### Mutation to update topics:
```graphql
mutation {
  updateTopics(input: {
    repositoryId: "YOUR_REPO_ID",
    topicNames: [
      "winget",
      "winget-pkgs",
      "windows-package-manager",
      "package-manager",
      "windows",
      "microsoft",
      "yaml",
      "manifest",
      "packages",
      "software-distribution",
      "winget-cli",
      "windows-installer",
      "msix",
      "msi",
      "appx",
      "hacktoberfest",
      "open-source",
      "community",
      "package-repository"
    ]
  }) {
    repository {
      repositoryTopics(first: 20) {
        nodes {
          topic {
            name
          }
        }
      }
    }
  }
}
```

**Using curl with GraphQL:**
```bash
curl -H "Authorization: bearer YOUR_GITHUB_TOKEN" \
  -X POST \
  -d '{"query":"mutation { updateTopics(input: { repositoryId: \"YOUR_REPO_ID\", topicNames: [\"winget\", \"winget-pkgs\", \"windows-package-manager\", \"package-manager\", \"windows\", \"microsoft\", \"yaml\", \"manifest\", \"packages\", \"software-distribution\", \"winget-cli\", \"windows-installer\", \"msix\", \"msi\", \"appx\", \"hacktoberfest\", \"open-source\", \"community\", \"package-repository\"] }) { repository { repositoryTopics(first: 20) { nodes { topic { name } } } } }"}' \
  https://api.github.com/graphql
```

---

### Method 5: Using Python (PyGithub)

```python
from github import Github

# Authenticate
g = Github("YOUR_GITHUB_TOKEN")

# Get the repository
repo = g.get_repo("Baneeishaque/winget-pkgs")

# Define topics
topics = [
    "winget",
    "winget-pkgs",
    "windows-package-manager",
    "package-manager",
    "windows",
    "microsoft",
    "yaml",
    "manifest",
    "packages",
    "software-distribution",
    "winget-cli",
    "windows-installer",
    "msix",
    "msi",
    "appx",
    "hacktoberfest",
    "open-source",
    "community",
    "package-repository"
]

# Replace all topics
repo.replace_topics(topics)

# Get current topics
print(repo.get_topics())
```

**Installation:**
```bash
pip install PyGithub
```

---

### Method 6: Using JavaScript (Octokit)

```javascript
const { Octokit } = require("@octokit/rest");

const octokit = new Octokit({
  auth: "YOUR_GITHUB_TOKEN"
});

async function setTopics() {
  const topics = [
    "winget",
    "winget-pkgs",
    "windows-package-manager",
    "package-manager",
    "windows",
    "microsoft",
    "yaml",
    "manifest",
    "packages",
    "software-distribution",
    "winget-cli",
    "windows-installer",
    "msix",
    "msi",
    "appx",
    "hacktoberfest",
    "open-source",
    "community",
    "package-repository"
  ];

  await octokit.repos.replaceAllTopics({
    owner: "Baneeishaque",
    repo: "winget-pkgs",
    names: topics
  });

  console.log("Topics updated successfully!");
}

setTopics();
```

**Installation:**
```bash
npm install @octokit/rest
```

---

### Method 7: Using PowerShell

```powershell
$token = "YOUR_GITHUB_TOKEN"
$owner = "Baneeishaque"
$repo = "winget-pkgs"

$topics = @(
    "winget",
    "winget-pkgs",
    "windows-package-manager",
    "package-manager",
    "windows",
    "microsoft",
    "yaml",
    "manifest",
    "packages",
    "software-distribution",
    "winget-cli",
    "windows-installer",
    "msix",
    "msi",
    "appx",
    "hacktoberfest",
    "open-source",
    "community",
    "package-repository"
)

$body = @{
    names = $topics
} | ConvertTo-Json

$headers = @{
    "Accept" = "application/vnd.github+json"
    "Authorization" = "Bearer $token"
    "X-GitHub-Api-Version" = "2022-11-28"
}

Invoke-RestMethod `
    -Uri "https://api.github.com/repos/$owner/$repo/topics" `
    -Method Put `
    -Headers $headers `
    -Body $body `
    -ContentType "application/json"
```

---

## Quick Reference: Complete Topic List

Copy this comma-separated list for easy use:

```
winget,winget-pkgs,windows-package-manager,package-manager,windows,microsoft,yaml,manifest,packages,software-distribution,winget-cli,windows-installer,msix,msi,appx,hacktoberfest,open-source,community,package-repository
```

## Notes

- GitHub allows a maximum of 20 topics per repository
- Topics must be lowercase
- Topics can only contain letters, numbers, and hyphens
- Topics must start with a letter or number
- Topics should be relevant and descriptive

## Related Links

- [GitHub Topics Documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics)
- [GitHub CLI Documentation](https://cli.github.com/manual/)
- [GitHub REST API - Topics](https://docs.github.com/en/rest/repos/repos#replace-all-repository-topics)
- [Windows Package Manager GitHub](https://github.com/microsoft/winget-cli)
