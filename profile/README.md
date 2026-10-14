# Grid

### Self-hosted infrastructure orchestration — desired-state JSON, Terraform modules, audited releases.

**Your control plane. Your credentials. Your state.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)

![Grid Banner](../readme-assets/banner.png)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../STATUS.md)**

[Quick start](#quick-start) · [How it works](#how-it-works) · [Repositories](#repositories) · [Documentation](#documentation)

---

Grid turns path-shaped infrastructure JSON into Terraform via a public module bank, runs **plan / apply / destroy** as audited **releases**, and ships a console for GitOps-style desired state. You self-host on a VM or with Docker Compose — no vendor lock-in, plain Terraform exit path.

> **Demo video** — coming soon.

## Quick start

1. Create **[remote Terraform state](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Install Grid on a VM (Compose by default).

```bash
export GRID_AUTH_ADMIN_PASSWORD='choose-a-strong-password'
# set GRID_TF_BACKEND / GRID_TF_STATE_BUCKET / … after remote state exists
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

Or from a clone:

```bash
git clone https://github.com/gridplatform/grid-core.git
cd grid-core
cp install/.env.example install/.env   # password + GRID_TF_*
docker compose -f install/docker-compose.yml --env-file install/.env up -d --build
```

Open `http://<host>/`. Prefer an **instance role / service account** on the VM over long-lived cloud keys.

Full path: **[Install on a VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## How it works

| Piece | Role |
|-------|------|
| Desired-state JSON | What to deploy (`grid-config` or your fork) |
| Module bank | Terraform modules (`grid-terraform`) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, GitOps sync, releases + live logs |
| grid-ui | Console |

Cloud permissions come from the **host identity** (AWS instance role / GCP ADC). Desired-state files do not carry credentials. Production uses remote state so a replaced VM does not lose the Terraform map.

## Repositories

| Repo | Role |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Console |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate / plan / apply / destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Module bank |
| [grid-config](https://github.com/gridplatform/grid-config) | Sample desired-state (GitOps) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Documentation |

Done / in progress / planned: **[STATUS.md](../STATUS.md)**.

## Documentation

| Guide | Link |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Contributing

Fork → branch → PR against `main`. See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md) and each repo’s guidelines.

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## License

MIT — see each repository’s `LICENSE`.
