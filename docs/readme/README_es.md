<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · **Español** · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### La plataforma de orquestación de infraestructura autoalojada.

**Hecha para que las empresas desplieguen y gestionen infraestructura — con el control en sus manos.**

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

Grid es una plataforma **autoalojada** para desplegar y operar infraestructura en la nube. Las empresas la usan para conservar cómo se despliega, quién puede cambiarlo y dónde vive el acceso — sin ceder ese control a la consola de otro proveedor.

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

Grid es donde tu equipo va a **pedir recursos en la nube** y **ver qué cambió de verdad**.

Escribes lo que quieres — una red, un servidor, una base de datos — en archivos de configuración en un repository de GitHub que **tú** posees. Grid lee esa descripción, muestra un plan de lo que cambiaría y, cuando apruebas, crea o elimina esos recursos en tu nube. Cada cambio se guarda como un release con logs en vivo, para que otros puedan seguirlo y mirarlo después.

Ejecutas Grid en hardware bajo **tu** control. El acceso a la nube queda con la identidad de esa máquina — tus configs no necesitan contraseñas ni claves dentro. Si más adelante sustituyes la máquina, el registro de lo que Grid gestiona sigue en el almacenamiento remoto que configuraste una vez.

En resumen: di lo que quieres, revisa el plan, aplica con un rastro en el que confiar.

## Tu estado deseado

**[grid-config](https://github.com/gridplatform/grid-config) es solo un ejemplo.** Úsalo para ver cómo se ven las configs. **No** lo forks para tu entorno real.

Para tu propio setup:

1. Crea un repositorio de GitHub **nuevo** en tu org o cuenta.
2. Pon ahí tus propios archivos de configuración (lo que quieres en cada entorno).
3. Apunta Grid a **ese** repository — no a `grid-config`.

Copia ideas del ejemplo; quédate con la propiedad del repository y de los ajustes.

## Repositorios

| Repositorio | Para qué sirve |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Ejecuta Grid en tu máquina — el motor detrás de escena y cómo instalarlo |
| [grid-ui](https://github.com/gridplatform/grid-ui) | El sitio web que usas en el navegador |
| [grid-cli](https://github.com/gridplatform/grid-cli) | El mismo trabajo desde una terminal, sin abrir el sitio |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Piezas listas para recursos cloud habituales (redes, servidores y más) |
| [grid-config](https://github.com/gridplatform/grid-config) | Configs de ejemplo para aprender — **no** tu setup real (crea tu propio repositorio) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Guías en lenguaje claro |

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

Haz fork de un repository de **producto** (core, ui, cli, terraform, docs) → rama → PR a `main`.  
No uses `grid-config` como tu home privado de estado deseado.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licencia

MIT — see each repository’s `LICENSE`.
