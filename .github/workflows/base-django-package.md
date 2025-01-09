# Base Django Package Workflow

This workflow provides a comprehensive CI/CD pipeline for Django packages, handling testing, building, and publishing processes.

## Requirements

- Add Secrets to the repository with the following keys

```text
- `DEVPI_TOKEN`: Token for private repository
- `PYPI_TOKEN`: PyPI authentication token
- `DEVPI_URL`: Private repository URL
```

## Inputs

| Input | Description | Required | Default | Options |
|-------|-------------|----------|---------|---------|
| `python-version` | Python version to use for building | No | `3.12` | - |
| `version-type` | Version type for the package | No | `CalVer` | `CalVer`, `SemVer` |

## Usage

```yaml
# .github/workflows/django-package.yml
name: Django Package CI/CD

on:
  push:
    branches: [
      main, # Push_case_1
      master, # Push_case_1
      develop, # Push_case_1
      staging, # Push_case_2
      production, # Push_case_3
    ]
    paths:
      - django_package_name/**

  pull_request:
    types: [opened, synchronize, reopened]
    branches: [
      main, # PR_case_1
      master, # PR_case_1
      develop, # PR_case_1
      staging, # PR_case_2
      production, # PR_case_3
    ]
    paths:
      - django_package_name/**

  release:
    types: [
        prereleased, # Release_case_1
        released, # Release_case_2
      ]

jobs:
  django-packaging:
    name: 📦 Django Packaging
    permissions:
      contents: write
      packages: write
    uses: actions-factory/risotech-github-actions/.github/workflows/base-django-package.yml@main
    secrets:
      DEVPI_URL: ${{ secrets.DEVPI_URL }}
      DEVPI_TOKEN: ${{ secrets.DEVPI_TOKEN }}
    with:
      python-version: ${{ vars.PYTHON_VERSION }}
      version-type: ${{ vars.VERSION_TYPE }}

```

## Description

This workflow provides a comprehensive CI/CD pipeline for Django packages, handling testing, building, and publishing processes. The workflow is triggered by push, pull request, and release events.

### Trigger Cases

#### Push Events

- **Push_case_1**: Main development branches (main, master, develop)
  - Triggers tests and build
  - No package publishing
- **Push_case_2**: Staging branch
  - Triggers tests, build, and pre-release package publishing
- **Push_case_3**: Production branch
  - Triggers tests, build, and stable package publishing

#### Pull Request Events

- **PR_case_1**: PRs to main development branches
  - Triggers tests and build validation
- **PR_case_2**: PRs to staging
  - Triggers tests and pre-release build validation
- **PR_case_3**: PRs to production
  - Triggers tests and stable build validation

#### Release Events

- **Release_case_1**: Pre-release
  - Triggers package publishing to pre-release channel
- **Release_case_2**: Release
  - Triggers package publishing to stable channel
