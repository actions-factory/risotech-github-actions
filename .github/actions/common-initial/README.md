# Common Initial Action

This GitHub Action performs common initialization steps for the workflow.

## Usage

```yaml
- uses: actions-factory/risotech-github-actions/.github/actions/common-initial@main
```

## Description

This action sets up the initial environment and configuration needed for the workflow execution. It handles common setup tasks required across different workflows.

## Inputs

- None

## Outputs

The action provides the following outputs:

- `repository_visibility`: The Repository is private or public
- `repository_name`: The name of the repository

## Example

```yaml
jobs:
  repository-information:
    name: 📊 Analysis repository information
    runs-on: ubuntu-latest
    outputs:
      repository_visibility: ${{ steps.common_initial.outputs.repository_visibility }}
      package_name: ${{ steps.common_initial.outputs.package_name }}
    steps:
    - name: 📥 Checkout Repository
      uses: actions/checkout@v4

    - name: 🔰 Initial Setup
      id: common_initial
      uses: actions-factory/risotech-github-actions/.github/actions/common-initial@main

    - name: 📢 Show Outputs
      run: |
        echo "This Repo is: ${{ steps.common_initial.outputs.repository_visibility }}"
        echo "This Repo Name is: ${{ steps.common_initial.outputs.repository_name }}"
```
