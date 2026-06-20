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
