<!-- # Grid Platform -->

![Grid Banner](../readme-assets/banner.png)

> **Infrastructure Orchestration Platform**  
> Open-source, self-hosted control plane for cloud infrastructure — desired-state JSON, Terraform modules, releases with live logs. No vendor lock-in.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/gridplatform/grid-core?style=social)](https://github.com/gridplatform/grid-core)

## What is Grid?

Grid turns path-shaped infrastructure JSON into Terraform via a public module bank, runs **plan / apply / destroy** as audited **releases**, and ships a console for GitOps-style desired state.

**Highlights**
- Self-hosted (your VM or Compose) — you keep credentials and state
- Multi-cloud modules in [grid-terraform](https://github.com/gridplatform/grid-terraform) (AWS, GCP, …)
- GitOps desired-state in [grid-config](https://github.com/gridplatform/grid-config) (or your fork)
- Fork → PR to contribute; `main` is protected by review + CI

## Public repositories

| Repository | Purpose | Status |
|------------|---------|--------|
| [grid-core](https://github.com/gridplatform/grid-core) | Control-plane API + install packaging | **Public** — active |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Console (React) | **Public** — active |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate / plan / apply / destroy | **Public** — active |
| [grid-config](https://github.com/gridplatform/grid-config) | Sample desired-state (GitOps) | **Public** — active |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform module bank | **Public** — active |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Docs on GitHub (Markdown-first) | **Public** — active |

### Later / not required for install

| Repository | Purpose | Status |
|------------|---------|--------|
| [grid-operator](https://github.com/gridplatform/grid-operator) | Kubernetes operator | Private — planned |
| [grid-ml](https://github.com/gridplatform/grid-ml) | ML / assistant features | Private — planned |

## Quick start — self-host

Docs are meant to be read **on GitHub** (no docs website required): **[grid-docs](https://github.com/gridplatform/grid-docs#readme)**

1. **[Remote Terraform state](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure)  
2. **[Install on a VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)** (Compose by default)  
3. **[Organizations guide](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md)**

```bash
git clone https://github.com/gridplatform/grid-core.git
cd grid-core
cp install/.env.example install/.env   # set GRID_AUTH_ADMIN_PASSWORD + GRID_TF_*
docker compose -f install/docker-compose.yml --env-file install/.env up -d --build
```

Or Ubuntu one-liner:

```bash
export GRID_AUTH_ADMIN_PASSWORD='choose-a-strong-password'
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

## Learn more

- [Documentation (grid-docs)](https://github.com/gridplatform/grid-docs)
- [Website](https://gridplatform.org)
- [Report issues](https://github.com/gridplatform/grid-core/issues)

## Contributing

Fork the repo → branch → open a pull request against `main`.  
See each repository’s `CONTRIBUTING.md` (and [grid-docs](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md)).

---

**Built with ❤️ by the open-source community**
