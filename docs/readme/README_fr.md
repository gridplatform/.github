<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · **Français** · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Orchestration d’infrastructure auto-hébergée — JSON d’état désiré, modules Terraform, releases auditées.

**Votre plan de contrôle. Vos identifiants. Votre état.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Démarrage rapide](#démarrage-rapide) · [Fonctionnement](#fonctionnement) · [Votre état désiré](#votre-état-désiré) · [Dépôts](#dépôts) · [Documentation](#documentation)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid transforme du JSON d’infra en forme de chemin en Terraform via une banque de modules publique, exécute **plan / apply / destroy** en **releases** auditées, et fournit une console style GitOps. Auto-hébergez sur une VM ou avec Docker Compose — sans verrouillage fournisseur, sortie Terraform pure.

> **Vidéo démo** — bientôt.

## Démarrage rapide

1. Créez l’**[état Terraform distant](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Installez Grid sur une VM (Compose par défaut).

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

Ouvrez `http://<host>/`. Préférez un **rôle d’instance / compte de service** sur la VM aux clés cloud longue durée.

Parcours complet : **[Installer sur une VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Fonctionnement

| Élément | Rôle |
|-------|------|
| **Votre** dépôt d’état désiré | Un dépôt GitHub que **vous** créez — JSON de ce que vous déployez |
| Banque de modules | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, sync GitOps, releases + logs live |
| grid-ui | Console |

Les permissions cloud viennent de l’**identité de l’hôte** (rôle d’instance AWS / ADC GCP). Les fichiers d’état désiré ne portent pas de secrets. La production utilise l’état distant pour qu’une VM remplacée ne perde pas la carte Terraform.

## Votre état désiré

**[grid-config](https://github.com/gridplatform/grid-config) n’est qu’un exemple.** Lisez-le pour la forme du JSON. Ne le **forkez pas** pour la production.

Pour un vrai déploiement :

1. Créez un **nouveau** dépôt GitHub sous votre org ou compte.
2. Ajoutez votre propre JSON en forme de chemin (provider / env / unités de ressource).
3. Pointez Grid vers ce dépôt (`GRID_GITOPS_REPO_URL`) — pas vers `grid-config`.

Copiez les motifs de l’exemple ; le dépôt et les réglages vous appartiennent.

## Dépôts

| Repo | Rôle |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Console |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | État désiré **d’exemple** (pas votre fork de prod) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Documentation |

Fait / en cours / prévu : **[STATUS.md](../../STATUS.md)**.

## Documentation

| Guide | Lien |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Contribuer

Forkez un dépôt **produit** (core, ui, cli, terraform, docs) → branche → PR vers `main`.  
Ne traitez pas `grid-config` comme votre dépôt privé d’état désiré.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues : [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licence

MIT — see each repository’s `LICENSE`.
