<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · **Deutsch** · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Die selbst gehostete Infrastruktur-Orchestrierungsplattform.

**Für Unternehmen, die Infrastruktur bereitstellen und betreiben — mit Kontrolle, die bei Ihnen bleibt.**

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

Grid ist eine **selbst gehostete** Plattform zum Bereitstellen und Betreiben von Cloud-Infrastruktur. Unternehmen behalten, wie Dinge ausgerollt werden, wer ändern darf und wo Zugänge liegen — ohne diese Kontrolle an die Cloud-Konsole eines anderen Anbieters abzugeben.

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

Grid ist der Ort, an dem Ihr Team **Cloud-Ressourcen anfordert** und **sieht, was sich wirklich geändert hat**.

Sie schreiben auf, was Sie wollen — Netzwerk, Server, Datenbank — in Konfigurationsdateien in einem GitHub-Repository, das **Ihnen** gehört. Grid liest diese Beschreibung, zeigt einen Plan der Änderungen und erstellt oder entfernt die Ressourcen in Ihrer Cloud, sobald Sie zustimmen. Jede Änderung wird als Release mit Live-Logs gespeichert, damit andere mitverfolgen und später nachschauen können.

Sie betreiben Grid auf Hardware unter **Ihrer** Kontrolle. Cloud-Zugang bleibt an der Identität dieser Maschine — Ihre Configs brauchen keine Passwörter oder Schlüssel darin. Wird die Maschine später ersetzt, bleibt der Überblick darüber, was Grid verwaltet, im Remote-Speicher, den Sie einmal eingerichtet haben.

Kurz: sagen, was Sie wollen, den Plan prüfen, mit einer Spur anwenden, der Sie vertrauen.

## Ihr Desired State

**[grid-config](https://github.com/gridplatform/grid-config) ist nur ein Beispiel.** Nutzen Sie es, um zu sehen, wie Configs aussehen. **Nicht** für Ihre echte Umgebung forken.

Für Ihr eigenes Setup:

1. Legen Sie ein **neues** GitHub-Repository unter Ihrer Org oder Ihrem Konto an.
2. Legen Sie Ihre eigenen Config-Dateien ab (was Sie in jeder Umgebung wollen).
3. Zeigen Sie Grid auf **dieses** Repository — nicht auf `grid-config`.

Ideen aus dem Beispiel übernehmen; Besitz von Repository und Einstellungen behalten.

## Repositories

| Repository | Wofür es da ist |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Lässt Grid auf Ihrem Rechner laufen — die Engine im Hintergrund und die Installation |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Die Website, die Sie im Browser nutzen |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Dieselbe Arbeit im Terminal, ohne die Website zu öffnen |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Fertige Bausteine für übliche Cloud-Ressourcen (Netze, Server und mehr) |
| [grid-config](https://github.com/gridplatform/grid-config) | Beispiel-Configs zum Lernen — **nicht** Ihr echtes Setup (legen Sie Ihr eigenes Repository an) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Leitfäden in klarer Sprache |

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

Forken Sie ein **Produkt**-Repository (core, ui, cli, terraform, docs) → Branch → PR gegen `main`.  
Nutzen Sie `grid-config` nicht als privates Desired-State-Zuhause.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Lizenz

MIT — see each repository’s `LICENSE`.
