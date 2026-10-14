<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · **Italiano**

# Grid Platform

### La piattaforma di orchestrazione infrastrutturale self-hosted.

**Pensata per le imprese che distribuiscono e gestiscono infrastruttura — con un controllo che resta vostro.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Avvio rapido](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [Come funziona](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [Il tuo stato desiderato](https://github.com/gridplatform/grid-config#readme) · [Repository](https://github.com/orgs/gridplatform/repositories) · [Documentazione](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid è una piattaforma **self-hosted** per distribuire e far girare infrastruttura cloud. Le imprese la usano per mantenere come si rilascia, chi può modificare e dove vive l’accesso — senza cedere quel controllo alla console di un altro fornitore.

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

Grid è dove il tuo team va a **chiedere risorse cloud** e **vedere cosa è davvero cambiato**.

Scrivi ciò che vuoi — una rete, un server, un database — in file di configurazione in un repository GitHub di **tua** proprietà. Grid legge quella descrizione, mostra un piano di cosa cambierebbe e, quando approvi, crea o rimuove quelle risorse nel tuo cloud. Ogni cambiamento viene salvato come release con log in diretta, così altri possono seguire e rivedere dopo.

Fai girare Grid su hardware sotto **il tuo** controllo. L’accesso al cloud resta con l’identità di quella macchina — i file di config non devono contenere password o chiavi. Se la macchina viene sostituita più avanti, il registro di ciò che Grid gestisce resta nello storage remoto che hai impostato una volta.

In breve: di’ cosa vuoi, rivedi il piano, applica con una traccia di cui fidarti.

## Il tuo stato desiderato

**[grid-config](https://github.com/gridplatform/grid-config) è solo un esempio.** Usalo per vedere come sono fatte le config. **Non** fare fork per il tuo ambiente reale.

Per il tuo setup:

1. Crea un repository GitHub **nuovo** sotto la tua org o account.
2. Metti lì i tuoi file di configurazione (cosa vuoi in ogni ambiente).
3. Punta Grid a **quel** repository — non a `grid-config`.

Prendi idee dall’esempio; resta proprietario del repository e delle impostazioni.

## Repository

| Repository | A cosa serve |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Fa girare Grid sulla tua macchina — il motore dietro le quinte e come installarlo |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Il sito web che usi nel browser |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Lo stesso lavoro da terminale, senza aprire il sito |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Pezzi pronti per risorse cloud comuni (reti, server e altro) |
| [grid-config](https://github.com/gridplatform/grid-config) | Config di esempio per imparare — **non** il tuo setup reale (crea il tuo repository) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Guide in linguaggio chiaro |

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

Fai fork di un repository di **prodotto** (core, ui, cli, terraform, docs) → branch → PR su `main`.  
Non trattare `grid-config` come casa privata del tuo stato desiderato.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licenza

MIT — see each repository’s `LICENSE`.
