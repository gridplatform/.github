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

O Grid ajuda você a **pedir, revisar e executar infraestrutura na nuvem você mesmo** — sem trancar seu setup no produto de outra pessoa. Você descreve o que quer, aprova mudanças com histórico claro e mantém acesso e registros em máquinas e armazenamento sob **seu** controle.

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

O Grid é onde sua equipe vai **pedir recursos na nuvem** e **ver o que realmente mudou**.

Você escreve o que quer — uma rede, um servidor, um banco — em arquivos de configuração num repositório GitHub que **você** possui. O Grid lê essa descrição, mostra um plano do que mudaria e, quando você aprova, cria ou remove esses recursos na sua nuvem. Cada mudança é salva como um release com logs ao vivo, para outros acompanharem e revisarem depois.

Você roda o Grid em hardware sob **seu** controle. O acesso à nuvem fica com a identidade dessa máquina — seus configs não precisam de senhas ou chaves dentro. Se a máquina for trocada depois, o registro do que o Grid gerencia continua no armazenamento remoto que você configurou uma vez.

Em resumo: diga o que quer, revise o plano, aplique com um rastro em que você confia.

## Seu estado desejado

**[grid-config](https://github.com/gridplatform/grid-config) é só um exemplo.** Use para ver como as configs parecem. **Não** faça fork para o seu ambiente real.

Para o seu próprio setup:

1. Crie um repositório GitHub **novo** na sua org ou conta.
2. Coloque seus próprios arquivos de configuração (o que você quer em cada ambiente).
3. Aponte o Grid para **esse** repository — não para `grid-config`.

Copie ideias do exemplo; fique com a propriedade do repository e das configurações.

## Documentação

| Guia | Link |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Contribuindo

Faça fork de um repository de **produto** (core, ui, cli, terraform, docs) → branch → PR em `main`.  
Não use `grid-config` como casa privada do seu estado desejado.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Licença

MIT — see each repository’s `LICENSE`.
