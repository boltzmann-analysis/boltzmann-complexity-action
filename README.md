# Boltzmann Complexity Action

A GitHub Action that analyzes code complexity changes in pull requests using the [Boltzmann Code Complexity Analyzer](https://boltzmann.co.uk).

## Features

- Compares complexity between base and head commits
- Posts a detailed PR comment with:
  - Overall complexity and density changes
  - File summary (added/deleted/modified/unchanged)
  - Complexity hotspots ranked by density
  - Complexity hotspots ranked by absolute change
  - Detailed file-by-file breakdown

## Usage

Add this to your workflow (e.g., `.github/workflows/complexity.yml`):

```yaml
name: Complexity Report

on:
  pull_request:
    branches: ["main"]

permissions:
  pull-requests: write
  contents: read

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: boltzmann-analysis/boltzmann-complexity-action@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `github-token` | GitHub token for posting PR comments | Yes | - |
| `repo-url` | Repository URL in `git@github.com:owner/repo.git` format | No | Current repo |
| `base-commit` | Base commit SHA | No | PR base commit |
| `head-commit` | Head commit SHA | No | PR head commit |
| `api-url` | Boltzmann API URL | No | `https://api.boltzmann.co.uk/compare` |

## Example Output

The action posts a comment like this on your PR:

---

## 📊 Boltzmann Complexity Analysis

**Repository:** `owner/repo`
**Comparison:** `abc1234` → `def5678`

### Overall Complexity

| Metric | Base | Head | Change |
|--------|------|------|--------|
| **Complexity** | 1234.56 | 1345.67 | 📈 +111.11 |
| **Density** | 0.4521 | 0.4612 | 📈 +0.0091 |

### File Summary

- 📄 **Files Added:** 2
- 🗑️ **Files Deleted:** 0
- ✏️ **Files Modified:** 5
- ✔️ **Files Unchanged:** 42

---

## License

MIT
