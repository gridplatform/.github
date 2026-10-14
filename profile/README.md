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

Grid helps you **request, review, and run cloud infrastructure yourself** — without locking your setup into someone else’s product. You describe what you want, approve changes with a clear history, and keep access and records on machines and storage **you** control.

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

Grid is where your team goes to **ask for cloud resources** and **see what actually changed**.

You write down what you want — a network, a server, a database — in config files stored in a GitHub repository **you** own. Grid reads that description, shows a plan of what would change, and when you approve, creates or removes those resources in your cloud. Every change is saved as a release with live logs, so people can follow along and look back later.

You run Grid on hardware **you** control. Cloud access stays with that machine’s identity — your config files do not need passwords or keys inside them. If the machine is replaced later, the record of what Grid manages still lives in remote storage you set up once.

In short: say what you want, review the plan, apply with a trail you can trust.

## Your desired state

**[grid-config](https://github.com/gridplatform/grid-config) is an example only.** Use it to see how configs look. Do **not** fork it for your real environment.

For your own setup:

1. Create a **new** GitHub repository under your org or account.
2. Put your own config files there (what you want in each environment).
3. Point Grid at **that** repository — not at `grid-config`.

Copy ideas from the example; keep ownership of the repository and the settings.

## Repositories

| Repository | Role |
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

Fork a **product** repository (core, ui, cli, terraform, docs) → branch → PR against `main`.  
Do not treat `grid-config` as your private desired-state home.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## License

MIT — see each repository’s `LICENSE`.
