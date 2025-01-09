# Python Linter Action

A GitHub Action that runs pre-commit linting checks on Python code.

## Usage

```yaml
- uses: actions-factory/riso-github-actions/.github/actions/python-linter@main
```

## Description

This action automates Python code linting using pre-commit hooks. It helps maintain consistent code quality by running configured linters and formatters as part of your GitHub Actions workflow.

## Requirements

- A `.pre-commit-config.yaml` file in your repository
- A `requirements.txt` file for Python dependencies

``` text
my-package/
├── .pre-commit-config.yaml
├── README.md
└── requirements.txt
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `python-version` | Python version to use | No | `3.12` |

## Example

```yaml
name: Lint Python Code
on: [push, pull_request]

jobs:
  python-linter:
    name: ⚡️ Python Lint
    runs-on: ubuntu-latest
    steps:
    - name: 📥 Checkout Repository
      uses: actions/checkout@v4

    - name: 🔍 Run Python Linter
      uses: actions-factory/risotech-github-actions/.github/actions/python-linter@main
      with:
        python-version: '3.12'
```
