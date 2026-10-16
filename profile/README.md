<div align="center">

**English** · [हिन्दी](../docs/readme/README_hi.md) · [简体中文](../docs/readme/README_zh.md) · [繁體中文](../docs/readme/README_zh-TW.md) · [日本語](../docs/readme/README_ja.md) · [한국어](../docs/readme/README_ko.md) · [Türkçe](../docs/readme/README_tr.md) · [Русский](../docs/readme/README_ru.md) · [Tiếng Việt](../docs/readme/README_vi.md) · [ไทย](../docs/readme/README_th.md) · [Deutsch](../docs/readme/README_de.md) · [Español](../docs/readme/README_es.md) · [Français](../docs/readme/README_fr.md) · [Українська](../docs/readme/README_uk.md) · [Polski](../docs/readme/README_pl.md) · [Português (Brasil)](../docs/readme/README_pt-BR.md) · [العربية](../docs/readme/README_ar.md) · [فارسی](../docs/readme/README_fa.md) · [Bahasa Indonesia](../docs/readme/README_id.md) · [Italiano](../docs/readme/README_it.md)

# Grid Platform

### The self-hosted infrastructure orchestration platform.

**Built for enterprises to deploy and manage infrastructure — with control that stays yours.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../STATUS.md)
[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-FFDD00?style=flat-square&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/thisiskushal)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../STATUS.md) · [Buy me a coffee](https://buymeacoffee.com/thisiskushal)**

[Quick start](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [How it works](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [Your desired state](https://github.com/gridplatform/grid-config#readme) · [Repositories](https://github.com/orgs/gridplatform/repositories) · [Documentation](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../readme-assets/banner.png)

</div>

---

Grid is a **self-hosted** platform for deploying and running cloud infrastructure. Enterprises use it to keep ownership of how things are rolled out, who can change them, and where access lives — without handing that control to another vendor’s cloud console.

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

| Repository | What it’s for |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Runs Grid on your machine — the engine behind the scenes, plus how you install it |
| [grid-ui](https://github.com/gridplatform/grid-ui) | The website you use in the browser |
| [grid-cli](https://github.com/gridplatform/grid-cli) | The same work from a terminal, without opening the website |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Ready-made pieces for common cloud resources (networks, servers, and more) |
| [grid-config](https://github.com/gridplatform/grid-config) | Sample configs to learn from — **not** your real setup (create your own repository) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Guides written in plain language |

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

[MIT](../LICENSE) © 2026 Grid Platform.

Product repositories (grid-core, grid-ui, grid-cli, and the rest) carry their own `LICENSE` files under the same terms.
