# Version Decision Action

This GitHub Action calculates and updates version numbers for Python packages using either Calendar Versioning (CalVer) or Semantic Versioning (SemVer).

## Usage

```yaml
- uses: actions-factory/risotech-github-actions/.github/actions/version-decision@main
```

## Description

### CalVer

Format: `YYYY.MMDD.COUNT[-STAGE]`

- Updates based on current date
- Increments COUNT if multiple releases on same day
- Optional stage suffix (-beta, -dev)

### SemVer

Format: `MAJOR.MINOR.PATCH[-STAGE]`

- Increments PATCH version
- Optional stage suffix (-beta, -dev)

## Inputs

| Name | Description | Required | Default | Options |
|------|-------------|----------|---------|----------|
| `package-name` | Name of the package for artifact | Yes | - | - |
| `deployment-stage` | Deployment stage | Yes | - | - |
| `deployment-type` | Deployment type | Yes | - | - |
| `version-type` | Type of versioning | No | `CalVer` | `CalVer`, `SemVer` |

## Outputs

| Name | Description |
|------|-------------|
| `version` | The calculated new version |
| `raw_version` | The calculated raw version |

## Example

```yaml
name: Version Update
on:
  push:
    branches:
      - main

jobs:
  version-decision:
    name: 🏷️ Version Decision
    needs: [ repository-information, deployment-decision ]
    if: needs.deployment-decision.outputs.should_deploy == 'true'
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
    - name: 📥 Checkout Repository
      uses: actions/checkout@v4
      with:
        fetch-depth: 0
        token: ${{ github.token }}

    - name: 🏷️ Version Decision
      id: version_decision
      uses: actions-factory/risotech-github-actions/.github/actions/version-decision@main
      with:
        package-name: ${{ needs.repository-information.outputs.package_name }}
        deployment-stage: ${{ needs.deployment-decision.outputs.deployment_stage }}
        version-type: CalVer

    - name: 📢 Show New Version
      run: |
        echo "New Version: ${{ steps.version_decision.outputs.version }}"
```
