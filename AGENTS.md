# AGENTS.md

Shared reusable GitHub Actions workflows for the CruGlobal-AI AppBuilder (AB) stack.

- Copied from the AB subset of `CruGlobal/.github`. Cru-wide infra workflows (ECS, Cloud Run, Lambda deploys) are left out on purpose. AI forks must never deploy into Cru infrastructure.
- Callers use `CruGlobal-AI/ab-workflows/.github/workflows/<name>.yml@main`.
- Images go to GHCR: `ghcr.io/cruglobal-ai/<image>`. `docker-build.yml` needs the calling job to grant `permissions: { contents: read, packages: write }` (org default token is read-only).
- Cross-repo auth uses the `cruglobal-ai-ab-ci` GitHub App. Org secrets: `DS_GH_APP_ID`, `DS_GH_APP_PK`.
- Most workflows use `github.repository_owner`, so they work in any org. Avoid hardcoding `CruGlobal` or `CruGlobal-AI`.

## Changes from upstream
- `docker-build.yml`: Docker Hub replaced with GHCR via `GITHUB_TOKEN`; Docker Hub secrets removed; optional `image` input; sets `org.opencontainers.image.source` so the package links to its repo.
- `cypress-e2e-tests.yml`: uses `CruGlobal-AI/ab-install-action@v1`.
