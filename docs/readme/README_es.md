<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · **Español** · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Orquestación de infraestructura autoalojada — JSON de estado deseado, módulos Terraform, releases auditables.

**Tu plano de control. Tus credenciales. Tu estado.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Inicio rápido](#inicio-rápido) · [Cómo funciona](#cómo-funciona) · [Tu estado deseado](#tu-estado-deseado) · [Repositorios](#repositorios) · [Documentación](#documentación)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid convierte JSON de infraestructura con forma de ruta en Terraform mediante un banco de módulos público, ejecuta **plan / apply / destroy** como **releases** auditables y ofrece una consola estilo GitOps. Autoalójaselo en una VM o con Docker Compose — sin dependencia del proveedor, salida a Terraform puro.

> **Vídeo demo** — próximamente.

## Inicio rápido

1. Crea el **[estado remoto de Terraform](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Instala Grid en una VM (Compose por defecto).

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

Abre `http://<host>/`. Prefiere un **rol de instancia / cuenta de servicio** en la VM frente a claves cloud longevas.

Ruta completa: **[Instalar en una VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Cómo funciona

| Pieza | Rol |
|-------|------|
| **Tu** repositorio de estado deseado | Un repo de GitHub que **tú** creas — JSON de lo que despliegas |
| Banco de módulos | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, sync GitOps, releases + logs en vivo |
| grid-ui | Consola |

Los permisos cloud vienen de la **identidad del host** (rol de instancia AWS / ADC de GCP). Los archivos de estado deseado no llevan credenciales. Producción usa estado remoto para que una VM reemplazada no pierda el mapa de Terraform.

## Tu estado deseado

**[grid-config](https://github.com/gridplatform/grid-config) es solo un ejemplo.** Léelo para aprender la forma del JSON. **No** lo forks para producción.

Para un despliegue real:

1. Crea un repositorio de GitHub **nuevo** en tu org o cuenta.
2. Añade tu propio JSON con forma de ruta (provider / env / unidades de recurso).
3. Apunta Grid a ese repo (`GRID_GITOPS_REPO_URL`) — no a `grid-config`.

Copia patrones del ejemplo; el repo y la configuración son tuyos.

## Repositorios

| Repo | Rol |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Consola |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | Estado deseado de **ejemplo** (no tu fork de producción) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Documentación |

Hecho / en curso / planificado: **[STATUS.md](../../STATUS.md)**.

## Documentación

| Guía | Enlace |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Contribuir

Haz fork de un repo de **producto** (core, ui, cli, terraform, docs) → rama → PR a `main`.  
No uses `grid-config` como tu home privado de estado deseado.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licencia

MIT — see each repository’s `LICENSE`.
