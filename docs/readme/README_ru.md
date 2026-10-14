<div align="center">

[English](../../profile/README.md) · [हिन्दी](README_hi.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · **Русский** · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Self-hosted платформа оркестрации инфраструктуры.

**Для предприятий, которые разворачивают и управляют инфраструктурой — с контролем, который остаётся у вас.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Быстрый старт](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [Как это работает](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [Ваш desired state](https://github.com/gridplatform/grid-config#readme) · [Репозитории](https://github.com/orgs/gridplatform/repositories) · [Документация](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid — это **self-hosted** платформа для развёртывания и работы облачной инфраструктуры. Предприятия используют её, чтобы сохранять, как всё выкатывается, кто может менять и где живёт доступ — не отдавая этот контроль чужой облачной консоли.

> **Демо-видео** — скоро.

## Быстрый старт

1. Создайте **[удалённый state Terraform](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Установите Grid на VM (по умолчанию Compose).

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

Откройте `http://<host>/`. Предпочитайте **instance role / service account** на VM вместо долгоживущих ключей.

Полный путь: **[Установка на VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Как это работает

Grid — это место, куда команда идёт **попросить облачные ресурсы** и **увидеть, что реально изменилось**.

Вы записываете, что хотите — сеть, сервер, базу — в файлах конфигурации в GitHub-репозитории, который **принадлежит вам**. Grid читает это описание, показывает план изменений и после вашего одобрения создаёт или удаляет ресурсы в вашем облаке. Каждое изменение сохраняется как релиз с live-логами, чтобы другие могли следить и потом пересмотреть.

Вы запускаете Grid на железе под **вашим** контролем. Доступ к облаку остаётся у личности этой машины — в конфигах не нужны пароли или ключи. Если машину потом заменят, запись о том, чем управляет Grid, останется в удалённом хранилище, которое вы один раз настроили.

Коротко: скажите, что нужно, проверьте план, примените с историей, которой можно доверять.

## Ваш desired state

**[grid-config](https://github.com/gridplatform/grid-config) — только пример.** Смотрите, как выглядят конфиги. **Не** форкайте для реального окружения.

Для своего setup:

1. Создайте **новый** GitHub-репозиторий в своей org или аккаунте.
2. Положите туда свои файлы конфигурации (что нужно в каждой среде).
3. Укажите Grid на **этот** репозиторий — не на `grid-config`.

Берите идеи из примера; владение репозиторием и настройками оставляйте себе.

## Репозитории

| Репозиторий | Для чего это |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Запускает Grid на вашей машине — движок за кулисами и способ установки |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Сайт, которым вы пользуетесь в браузере |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Та же работа из терминала, без открытия сайта |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Готовые блоки для обычных облачных ресурсов (сети, серверы и другое) |
| [grid-config](https://github.com/gridplatform/grid-config) | Пример конфигов для обучения — **не** ваш реальный setup (создайте свой репозиторий) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Руководства простым языком |

Сделано / в работе / запланировано: **[STATUS.md](../../STATUS.md)**.

## Документация

| Гид | Ссылка |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Участие

Форкните **продуктовый** репозиторий (core, ui, cli, terraform, docs) → ветка → PR в `main`.  
Не используйте `grid-config` как личный desired-state.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Лицензия

MIT — see each repository’s `LICENSE`.
