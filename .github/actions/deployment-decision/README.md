# Deployment Decision Action

This GitHub Action determines deployment strategies based on event triggers and branch contexts.

## Usage

```yaml
- uses: actions-factory/risotech-github-actions/.github/actions/deployment-decision@main
```

## Description

### Push Events

- `main/master/develop` → dev stage (direct)
- `staging` → beta stage (prerelease)
- `production` → production stage (release)

### Release Events

- `prereleased` → beta stage (prerelease)
- `released` → production stage (release)

### Deployment Types

- `direct`: Immediate deployment to development environment
- `prerelease`: Beta deployment with pre-release features
- `release`: Production deployment with stable features
- `skip`: No deployment needed

## Inputs

- None

## Outputs

| Name | Description |
|------|-------------|
| `should_deploy` | Boolean flag indicating if deployment should proceed (`true`/`false`) |
| `deployment_stage` | Target deployment stage (`alpha`/`beta`/`production`/`unknown`) |
| `deployment_type` | Type of deployment process (`direct`/`prerelease`/`release`/`skip`) |

## Example

```yaml
name: Deployment Decision Example
on:
  push:
    branches: [main, dev, staging, production]
  release:
    types: [prereleased, released]

jobs:
  deployment-decision:
    name: 🚀 Deploy Decision
    needs: [python-linter, pytest-coverage]
    runs-on: ubuntu-latest
    outputs:
      should_deploy: ${{ steps.deployment_decision.outputs.should_deploy }}
      deployment_stage: ${{ steps.deployment_decision.outputs.deployment_stage }}
      deployment_type: ${{ steps.deployment_decision.outputs.deployment_type }}
    steps:
    - name: 🎯 Deploy Strategy
      id: deployment_decision
      uses: actions-factory/risotech-github-actions/.github/actions/deployment-decision@main

    - name: 📢 Show Deploy Info
      run: |
        echo "Should Deploy: ${{ steps.deployment_decision.outputs.should_deploy }}"
        echo "Stage: ${{ steps.deployment_decision.outputs.deployment_stage }}"
        echo "Type: ${{ steps.deployment_decision.outputs.deployment_type }}"
```
