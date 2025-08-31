# YallaSystems Organization Workflows

This repository contains reusable GitHub workflows for the YallaSystems organization.

## Available Reusable Workflows

### 1. Reusable CI Workflow (`reusable-ci.yml`)

Runs continuous integration checks including build, lint, typecheck, and tests.

**Usage:**
```yaml
name: CI
on:
  pull_request:
    branches: [main]
  push:
    branches-ignore: [main]

jobs:
  ci:
    uses: YallaSystems/.github/.github/workflows/reusable-ci.yml@main
    with:
      build-command: 'npm run build'
      test-command: 'npm test'
    secrets: inherit
```

### 2. Reusable Release Workflow (`reusable-release.yml`)

Handles version bumping and package publishing when code is merged to main.

**Usage:**
```yaml
name: Release
on:
  push:
    branches: [main]

jobs:
  release:
    uses: YallaSystems/.github/.github/workflows/reusable-release.yml@main
    with:
      version-type: 'patch'
      build-command: 'npm run build'
    secrets: inherit
```

## Inputs

Both workflows support customizable inputs for different project requirements:

- `node-version`: Node.js version (default: '22')
- `build-command`: Build command (default: 'npm run build')
- `test-command`: Test command (default: 'npm test')
- `lint-command`: Lint command (default: 'npm run lint')
- `typecheck-command`: Type check command (default: 'npm run typecheck')
- `skip-tests`: Skip tests (default: false)
- `skip-lint`: Skip linting (default: false)
- `skip-typecheck`: Skip type checking (default: false)
- `version-type`: Version bump type - patch/minor/major (default: 'patch')

## Features

- **Automatic version conflict detection**: Checks if version already exists before publishing
- **Consistent authentication**: Uses GITHUB_TOKEN throughout
- **Flexible configuration**: Customizable commands and steps per repository
- **Smart version bumping**: Only bumps version if current version already exists in registry