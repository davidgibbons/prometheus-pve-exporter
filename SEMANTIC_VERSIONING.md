# Semantic Versioning for Prometheus PVE Exporter Helm Chart

This repository uses [Semantic Release](https://semantic-release.gitbook.io/) to automatically manage chart versions based on [Conventional Commits](https://www.conventionalcommits.org/).

## How It Works

1. **Semantic Release Workflow**: Analyzes commit messages and automatically determines the next version number
2. **Chart Release Workflow**: Packages and publishes the Helm chart to GitHub Pages

## Commit Message Format

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Commit Types and Version Bumps

| Commit Type | Version Bump | Example |
|-------------|--------------|---------|
| `feat:` | **Minor** (1.0.0 → 1.1.0) | `feat: add support for environment variables` |
| `fix:` | **Patch** (1.0.0 → 1.0.1) | `fix: resolve YAML parsing error in scrapeconfigs` |
| `perf:` | **Patch** (1.0.0 → 1.0.1) | `perf: optimize resource usage` |
| `refactor:` | **Patch** (1.0.0 → 1.0.1) | `refactor: improve code structure` |
| `BREAKING CHANGE:` | **Major** (1.0.0 → 2.0.0) | `feat!: remove deprecated API` |

### Non-Release Types

These commit types will **NOT** trigger a release:
- `docs:` - Documentation changes
- `style:` - Code style changes
- `chore:` - Maintenance tasks
- `test:` - Test additions/modifications
- `build:` - Build system changes
- `ci:` - CI/CD changes

## Examples

### Feature Addition (Minor Version Bump)
```
feat: add optional environment variable support

- Add env section to deployment template
- Update values.yaml with examples
- Support both simple and complex env vars
```

### Bug Fix (Patch Version Bump)
```
fix: correct YAML syntax in scrapeconfigs template

Fixed sourceLabels typo that was causing parsing errors
```

### Breaking Change (Major Version Bump)
```
feat!: upgrade to Kubernetes 1.25+ API versions

BREAKING CHANGE: This chart now requires Kubernetes 1.25 or higher
```

## Manual Release

You can manually trigger a release by:

1. **Push to main**: Any push to the main branch will trigger the semantic release workflow
2. **Manual workflow dispatch**: Go to Actions → Semantic Release → Run workflow

## Generated Files

The semantic release process automatically:
- Updates `charts/promtheus-pve-exporter/Chart.yaml` version
- Generates/updates `CHANGELOG.md`
- Creates Git tags
- Generates GitHub releases
- Triggers the Helm chart release workflow

## Skipping CI

To prevent the release workflow from running on semantic release commits, they include `[skip ci]` in the commit message. 