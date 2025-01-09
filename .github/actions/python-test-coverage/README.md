# Python Test Coverage Action

An automated GitHub Action that executes PyTest for Python projects, generates test coverage reports, and optionally uploads results to Codecov. The action simplifies the test coverage workflow by handling test execution, report generation, and coverage tracking in one step.

## Usage

```yaml
- uses: actions-factory/risotech-github-actions/.github/actions/python-test-coverage@main
```

## Description

The action will:

1. Run tests using PyTest
2. Generate coverage reports
3. Either:
     - Upload coverage to Codecov (if token provided)
     - Save coverage report as artifact (if no token)

## Requirements

- `requirements.txt` file in your repository

``` text
my-package/
├── pyproject.toml
├── README.md
└── requirements.txt
```

- PyTest and Coverage configured in your project
- (Optional) Add CODECOV_TOKEN to repository secrect

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `python-version` | Python version to use | No | `3.12` |
| `codecov-token` | Codecov token for coverage upload | No | - |

## Example

```yaml
name: Test Coverage

on: [push, pull_request]

jobs:
  pytest-coverage:
    name: 🧪 Test Coverage with PyTest
    needs: python-linter  # Optional: Add linter job as dependency
    runs-on: ubuntu-latest
    steps:
    - name: 📥 Checkout Repository
      uses: actions/checkout@v4

    - name: 🧪 Run PyTest with Coverage Report
      uses: actions-factory/risotech-github-actions/.github/actions/python-test-coverage@main
      with:
        python-version: '3.12'
        codecov-token: ${{ secrets.CODECOV_TOKEN }}
```
