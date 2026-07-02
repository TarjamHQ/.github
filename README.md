# TarjamHQ shared automation

Reusable GitHub Actions workflows for Tarjam repositories live in
`.github/workflows`.

## Node CI

Call the shared test, coverage, and build workflow from an application:

```yaml
jobs:
  ci:
    uses: TarjamHQ/.github/.github/workflows/node-ci.yml@main
    with:
      build-artifact-name: tarjam-app-build
```

The calling repository controls workflow triggers, permissions, concurrency,
commands, working directory, and artifact names through workflow inputs.

For an npm repository:

```yaml
jobs:
  ci:
    uses: TarjamHQ/.github/.github/workflows/node-ci.yml@main
    with:
      package-manager: npm
      lockfile-path: package-lock.json
      install-command: npm ci
      test-command: npm run test:cov
      build-command: npm run build
```

## Python Static Analysis

Call the shared ruff/mypy workflow from a Python application:

```yaml
jobs:
  static-analysis:
    uses: TarjamHQ/.github/.github/workflows/python-static-analysis.yml@main
    with:
      install-command: uv sync --locked
      typecheck-command: uv run mypy .
```

The calling repository controls the working directory, install command, and
which checks run — `ruff-check-command`, `ruff-format-command`, and
`typecheck-command` each skip their step when set to an empty string.
