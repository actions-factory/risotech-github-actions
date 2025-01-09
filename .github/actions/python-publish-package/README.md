# Python Publish Package Action

This GitHub Action publishes Python packages to PyPI (Python Package Index).

## Usage

```yaml
- uses: actions-factory/risotech-github-actions/.github/actions/python-publish-package@main
```

## Description

It automates the process of uploading your Python package distributions to PyPI, making it easier to release new versions of your packages.

## Requirements

- PyPI authentication token
- Artifacts from `python-build-package` action

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `package-name` | Name of the package to be published | Yes | - |
| `pypi-url` | PyPI repository URL | No | `https://upload.pypi.org/legacy/` |
| `pypi-token` | PyPI authentication token | Yes | - |

## Outputs

- Package file in PyPI repository

## Example

```yaml
name: Publish Package
on:
  release:
    types: [published]

jobs:
  python-publish:
    name: 📦 Publish Package
    needs: [ repository-information, python-build]
    runs-on: ubuntu-latest
    permissions:
      packages: read
      contents: read
    steps:
    - name: 🚀 Publish to PyPI
      uses: actions-factory/risotech-github-actions/.github/actions/python-publish-package@main
      with:
        package-name: ${{ needs.repository-information.outputs.package_name }}
        pypi-url: ${{ vars.DEVPI_URL }}
        pypi-token: ${{ secrets.PYPI_TOKEN }} # ${{ secrets.DEVPI_TOKEN }}
```
