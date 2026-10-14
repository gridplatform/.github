<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · **Português (Brasil)** · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Orquestração de infraestrutura self-hosted — JSON de estado desejado, módulos Terraform, releases auditáveis.

**Seu plano de controle. Suas credenciais. Seu estado.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Início rápido](#início-rápido) · [Como funciona](#como-funciona) · [Seu estado desejado](#seu-estado-desejado) · [Repositórios](#repositórios) · [Documentação](#documentação)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

O Grid transforma JSON de infra em forma de caminho em Terraform via um banco público de módulos, executa **plan / apply / destroy** como **releases** auditáveis e oferece um console estilo GitOps. Self-host em VM ou Docker Compose — sem lock-in, saída para Terraform puro.

> **Vídeo demo** — em breve.

## Início rápido

1. Crie o **[estado remoto do Terraform](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Instale o Grid em uma VM (Compose por padrão).

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

Abra `http://<host>/`. Prefira **papel de instância / conta de serviço** na VM a chaves cloud de longa duração.

Caminho completo: **[Instalar em uma VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Como funciona

| Peça | Papel |
|-------|------|
| **Seu** repositório de estado desejado | Um repo GitHub que **você** cria — JSON do que você implanta |
| Banco de módulos | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, sync GitOps, releases + logs ao vivo |
| grid-ui | Console |

Permissões cloud vêm da **identidade do host** (papel de instância AWS / ADC GCP). Arquivos de estado desejado não carregam credenciais. Produção usa estado remoto para que uma VM substituída não perca o mapa Terraform.

## Seu estado desejado

**[grid-config](https://github.com/gridplatform/grid-config) é só um exemplo.** Leia para aprender a forma do JSON. **Não** faça fork para produção.

Para um deploy real:

1. Crie um repositório GitHub **novo** na sua org ou conta.
2. Adicione seu próprio JSON em forma de caminho (provider / env / unidades de recurso).
3. Aponte o Grid para esse repo (`GRID_GITOPS_REPO_URL`) — não para `grid-config`.

Copie padrões do exemplo; o repo e as configs são seus.

## Repositórios

| Repo | Papel |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Console |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | Estado desejado de **exemplo** (não seu fork de produção) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Documentação |

Feito / em andamento / planejado: **[STATUS.md](../../STATUS.md)**.

## Documentação

| Guia | Link |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Contribuindo

Faça fork de um repo de **produto** (core, ui, cli, terraform, docs) → branch → PR em `main`.  
Não use `grid-config` como casa privada do seu estado desejado.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licença

MIT — see each repository’s `LICENSE`.
