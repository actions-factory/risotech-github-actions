# Python Build Package Action

This GitHub Action builds release distributions for a Python package.

## Usage

```yaml
- uses: actions-factory/risotech-github-actions/.github/actions/python-build-package@main
```

## Description

1. Sets up Python environment with specified version
2. Configures pip caching using `requirements.txt`
3. Builds package distributions using `build` tool
4. Uploads built distributions as artifacts

## Requirements

- `requirements.txt` file in repository root
- Valid Python package structure

``` text
my-package/
├── pyproject.toml
├── README.md
└── requirements.txt
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `python-version` | Python version to use for building | No | `3.12` |
| `package-name` | Name of the package for artifact | Yes | - |
| `new-version` | New version of artifact | Yes | - |
| `raw-version` | Raw version of artifact | Yes | - |
| `commit-bump` | Commit bump version or not | Yes | - |

## Outputs

- Package file in Github Actions Artifacts

## Example

```yaml
name: Build Package

jobs:
  python-build:
    name: 🏗️ Build Package
    needs: [ repository-information, version-decision]
    runs-on: ubuntu-latest
    permissions:
      packages: write
      contents: read
    steps:
    - name: 📥 Checkout Repository
      uses: actions/checkout@v4

    - name: 📦 Build Python Package
      uses: actions-factory/risotech-github-actions/.github/actions/python-build-package@main
      with:
        python-version: '3.12'
        package-name: ${{ needs.repository-information.outputs.package_name }}
        new-version: ${{ needs.version-decision.outputs.version }}
        raw-version: ${{ needs.version-decision.outputs.raw_version }}
        commit-bump: ${{ needs.version-decision.outputs.commit_bump }}
```
