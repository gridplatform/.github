<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · **Deutsch** · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Selbst gehostete Infrastruktur-Orchestrierung — Desired-State-JSON, Terraform-Module, auditierbare Releases.

**Ihre Control Plane. Ihre Zugangsdaten. Ihr State.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Schnellstart](#schnellstart) · [So funktioniert es](#so-funktioniert-es) · [Ihr Desired State](#ihr-desired-state) · [Repositories](#repositories) · [Dokumentation](#dokumentation)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid wandelt pfadförmiges Infrastruktur-JSON über eine öffentliche Modulbank in Terraform um, führt **plan / apply / destroy** als auditierbare **Releases** aus und liefert eine GitOps-Konsole. Self-Host auf VM oder Docker Compose — kein Vendor-Lock-in, reiner Terraform-Ausstieg.

> **Demo-Video** — demnächst.

## Schnellstart

1. **[Remote-Terraform-State](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** anlegen (S3 / GCS / Azure).
2. Grid auf einer VM installieren (Standard: Compose).

```bash
export GRID_AUTH_ADMIN_PASSWORD='choose-a-strong-password'
# set GRID_TF_BACKEND / GRID_TF_STATE_BUCKET / … after remote state exists
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

```bash
git clone https://github.com/gridplatform/grid-core.git
cd grid-core
cp install/.env.example install/.env   # password + GRID_TF_*
docker compose -f install/docker-compose.yml --env-file install/.env up -d --build
```

`http://<host>/` öffnen. Bevorzugen Sie **Instance Role / Service Account** auf der VM statt langlebiger Cloud-Keys.

Vollständig: **[Installation auf einer VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## So funktioniert es

| Teil | Rolle |
|-------|------|
| **Ihr** Desired-State-Repo | Ein GitHub-Repo, das **Sie** anlegen — JSON für das, was Sie deployen |
| Modulbank | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, GitOps-Sync, Releases + Live-Logs |
| grid-ui | Konsole |

Cloud-Berechtigungen kommen von der **Host-Identität** (AWS Instance Role / GCP ADC). Desired-State-Dateien tragen keine Credentials. Produktion nutzt Remote State, damit ein ersetzter VM den Terraform-Plan nicht verliert.

## Ihr Desired State

**[grid-config](https://github.com/gridplatform/grid-config) ist nur ein Beispiel.** Lesen Sie es für die JSON-Form. **Nicht** für Produktion forken.

Für ein echtes Deploy:

1. Legen Sie ein **neues** GitHub-Repository unter Ihrer Org oder Ihrem Konto an.
2. Fügen Sie Ihr eigenes pfadförmiges JSON hinzu (Provider / Env / Ressourceneinheiten).
3. Zeigen Sie Grid auf dieses Repo (`GRID_GITOPS_REPO_URL`) — nicht auf `grid-config`.

Muster aus dem Beispiel kopieren; Repo und Einstellungen gehören Ihnen.

## Repositories

| Repo | Rolle |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Konsole |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | **Beispiel**-Desired-State (kein Produktions-Fork) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Dokumentation |

Erledigt / in Arbeit / geplant: **[STATUS.md](../../STATUS.md)**.

## Dokumentation

| Leitfaden | Link |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Mitwirken

Forken Sie ein **Produkt**-Repo (core, ui, cli, terraform, docs) → Branch → PR gegen `main`.  
Nutzen Sie `grid-config` nicht als privates Desired-State-Zuhause.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Lizenz

MIT — see each repository’s `LICENSE`.
