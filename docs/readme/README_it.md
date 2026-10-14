<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · **Italiano**

# Grid Platform

### Orchestrazione infrastrutturale self-hosted — JSON di stato desiderato, moduli Terraform, release verificabili.

**Il tuo control plane. Le tue credenziali. Il tuo stato.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Avvio rapido](#avvio-rapido) · [Come funziona](#come-funziona) · [Il tuo stato desiderato](#il-tuo-stato-desiderato) · [Repository](#repository) · [Documentazione](#documentazione)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid trasforma JSON di infrastruttura a forma di percorso in Terraform tramite una banca moduli pubblica, esegue **plan / apply / destroy** come **release** verificabili e offre una console in stile GitOps. Self-host su VM o Docker Compose — senza vendor lock-in, uscita con Terraform puro.

> **Video demo** — in arrivo.

## Avvio rapido

1. Crea lo **[stato Terraform remoto](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Installa Grid su una VM (Compose di default).

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

Apri `http://<host>/`. Preferisci un **ruolo istanza / service account** sulla VM rispetto a chiavi cloud di lunga durata.

Percorso completo: **[Installare su una VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Come funziona

| Parte | Ruolo |
|-------|------|
| **Il tuo** repository di stato desiderato | Un repo GitHub che **crei tu** — JSON di ciò che deployi |
| Banca moduli | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, sync GitOps, release + log live |
| grid-ui | Console |

I permessi cloud arrivano dall’**identità dell’host** (ruolo istanza AWS / ADC GCP). I file di stato desiderato non portano credenziali. In produzione usi lo stato remoto così una VM sostituita non perde la mappa Terraform.

## Il tuo stato desiderato

**[grid-config](https://github.com/gridplatform/grid-config) è solo un esempio.** Leggilo per imparare la forma del JSON. **Non** fare fork per la produzione.

Per un deploy reale:

1. Crea un repository GitHub **nuovo** sotto la tua org o account.
2. Aggiungi il tuo JSON a forma di percorso (provider / env / unità di risorsa).
3. Punta Grid a quel repo (`GRID_GITOPS_REPO_URL`) — non a `grid-config`.

Copia i pattern dall’esempio; il repo e le impostazioni sono tuoi.

## Repository

| Repo | Ruolo |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Console |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | Stato desiderato di **esempio** (non il tuo fork di produzione) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Documentazione |

Fatto / in corso / pianificato: **[STATUS.md](../../STATUS.md)**.

## Documentazione

| Guida | Link |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Contribuire

Fai fork di un repo di **prodotto** (core, ui, cli, terraform, docs) → branch → PR su `main`.  
Non trattare `grid-config` come casa privata del tuo stato desiderato.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licenza

MIT — see each repository’s `LICENSE`.
