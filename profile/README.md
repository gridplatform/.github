<div align="center">

**English** · [简体中文](../docs/readme/README_zh.md) · [繁體中文](../docs/readme/README_zh-TW.md) · [日本語](../docs/readme/README_ja.md) · [한국어](../docs/readme/README_ko.md) · [Türkçe](../docs/readme/README_tr.md) · [Русский](../docs/readme/README_ru.md) · [Tiếng Việt](../docs/readme/README_vi.md) · [ไทย](../docs/readme/README_th.md) · [Deutsch](../docs/readme/README_de.md) · [Español](../docs/readme/README_es.md) · [Français](../docs/readme/README_fr.md) · [Українська](../docs/readme/README_uk.md) · [Polski](../docs/readme/README_pl.md) · [Português (Brasil)](../docs/readme/README_pt-BR.md) · [العربية](../docs/readme/README_ar.md) · [فارسی](../docs/readme/README_fa.md) · [Bahasa Indonesia](../docs/readme/README_id.md) · [Italiano](../docs/readme/README_it.md)

# Grid Platform

### Self-hosted infrastructure orchestration — desired-state JSON, Terraform modules, audited releases.

**Your control plane. Your credentials. Your state.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../STATUS.md)**

[Quick start](#quick-start) · [How it works](#how-it-works) · [Your desired state](#your-desired-state) · [Repositories](#repositories) · [Documentation](#documentation)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../readme-assets/banner.png)

</div>

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
| **Your** desired-state repo | GitHub repo you create — JSON for what you deploy |
| Module bank | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, GitOps sync, releases + live logs |
| grid-ui | Console |

Cloud permissions come from the **host identity** (AWS instance role / GCP ADC). Desired-state files do not carry credentials. Production uses remote state so a replaced VM does not lose the Terraform map.

## Your desired state

**[grid-config](https://github.com/gridplatform/grid-config) is an example only.** Read it to learn the JSON shape. Do **not** fork it for production.

For a real deploy:

1. Create a **new** GitHub repository under your org or account.
2. Add your own path-shaped JSON (provider / env / resource units).
3. Point Grid at that repo (`GRID_GITOPS_REPO_URL`) — not at `grid-config`.

Copy patterns from the example; own the repo and the settings.

## Repositories

| Repo | Role |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Console |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate / plan / apply / destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Module bank |
| [grid-config](https://github.com/gridplatform/grid-config) | **Example** desired-state (not your production fork) |
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

Fork a **product** repo (core, ui, cli, terraform, docs) → branch → PR against `main`.  
Do not treat `grid-config` as your private desired-state home.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## License

MIT — see each repository’s `LICENSE`.
