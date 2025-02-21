# Riso Tech Github Actions

This repository contains the Github Actions reusable actions/workflows.

## Available Actions

### Common Initial Action

Performs common initialization steps for workflows. [Learn more](/.github/actions/common-initial/README.md)

### Python Linter Action

Runs pre-commit linting checks on Python code. [Learn more](/.github/actions/python-linter/README.md)

### Python Test Coverage Action

Executes PyTest for Python projects and generates test coverage reports. [Learn more](/.github/actions/python-test-coverage/README.md)

### Deployment Decision Action

Determines deployment strategies based on event triggers and branch contexts. [Learn more](/.github/actions/deployment-decision/README.md)

### Version Decision Action

Calculates version numbers for Python packages using CalVer or SemVer formats. [Learn more](/.github/actions/version-decision/README.md)

### Python Build Package Action

Builds release distributions for Python packages, managing version updates and artifact generation. [Learn more](/.github/actions/python-build/README.md)

### Python Publish Package Action

Publishes Python packages to PyPI, handling authentication and distribution uploads. [Learn more](/.github/actions/python-publish-package/README.md)

## Available Workflows

### Django Package CI/CD Workflow

A complete CI/CD workflow for Django packages, including linting, testing, and deployment. [Learn more](/.github/workflows/base-django-package.yml)

## Usage

Each action has its own documentation with specific usage instructions. Navigate to the action's directory for detailed information.
