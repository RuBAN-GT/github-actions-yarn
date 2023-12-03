# Github Actions - Yarn

The repository provides utils helping to organize your project GitHub actions environment using actual Yarn package manager: re-usable workflows and actions.

## Custom Actions

### 1. Setup Yarn Publish Configuration

- **Name**: `setup-env`
- **Description**: Setup and configure Yarn publish configuration.
- **Inputs**:
  - `npm-registry`: Private NPM registry URL (default: `https://npm.pkg.github.com`).
- **Example**:

```yml
- uses: RuBAN-GT/github-actions-yarn/.github/actions/setup-env
  with:
    npm-registry: https://npm.pkg.github.com
```

### 2. Setup Yarn Environment

- **Name**: `setup-yarn`
- **Description**: Setup and configure Yarn project environment.
- **Inputs**:
  - `node-version`: Node.js version to use (default: `"20.x"`).
- **Example**:

```yml
- uses: RuBAN-GT/github-actions-yarn/.github/actions/setup-yarn
  with:
    node-version: 20.x
```

### 3. Build Yarn Project

- **Name**: `yarn-build`
- **Description**: Build project content using Yarn.
- **Inputs**:
  - `project-type`: Specifies if the project is a `monorepo` or `singlerepo` (default: `singlerepo`).
- **Example**:

```yml
- uses: RuBAN-GT/github-actions-yarn/.github/actions/yarn-build
  with:
    project-type: singlerepo
```

### 4. Publish Yarn Libraries

- **Name**: `yarn-publish`
- **Description**: Publish project artifacts using Yarn.
- **Inputs**:
  - `project-type`: Specifies if the project is a `monorepo` or `singlerepo` (default: `singlerepo`).
- **Example**:

```yml
- uses: RuBAN-GT/github-actions-yarn/.github/actions/yarn-publish
  with:
    project-type: singlerepo
```

## Workflows

- Monorepo Workflow: `.github/workflows/yarn.monorepo.yml`
- Single Project Workflow: `.github/workflows/yarn.single.yml`

### Inputs

Inputs are identical for both workflows.

| Parameter        | Type    | Default                      | Comment                          |
| ---------------- | ------- | ---------------------------- | -------------------------------- |
| `runs-on`        | string  | `ubuntu-latest`              | Machine type for jobs            |
| `is-self-hosted` | boolean | `false`                      | If a self-hosted machine is used |
| `needs-release`  | boolean | `true`                       | If release flow is needed        |
| `node-version`   | string  | `"20.x"`                     | Node.js version                  |
| `npm-token-key`  | string  | `NPM_AUTH_TOKEN`             | Secret npm token key name        |
| `npm-registry`   | string  | `https://npm.pkg.github.com` | Private NPM registry URL         |

### Example Usage

```yaml
name: My workflow

on: [push, pull_request]

jobs:
  deploy:
    uses: RuBAN-GT/github-actions-yarn/workflows/yarn.monorepo.yml@main
    with:
      node-version: "18.x"
```
