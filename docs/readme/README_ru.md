<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · **Русский** · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Self-hosted оркестрация инфраструктуры — JSON желаемого состояния, модули Terraform, аудируемые релизы.

**Ваша control plane. Ваши учётные данные. Ваше состояние.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Быстрый старт](#быстрый-старт) · [Как это работает](#как-это-работает) · [Ваш desired state](#ваш-desired-state) · [Репозитории](#репозитории) · [Документация](#документация)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid превращает path-shaped JSON инфраструктуры в Terraform через публичный банк модулей, выполняет **plan / apply / destroy** как аудируемые **releases** и даёт консоль в стиле GitOps. Self-host на VM или Docker Compose — без vendor lock-in, выход через чистый Terraform.

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

| Часть | Роль |
|-------|------|
| **Ваш** репозиторий desired-state | GitHub-репозиторий, который **создаёте вы** — JSON того, что деплоите |
| Банк модулей | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, GitOps-синхронизация, релизы + live-логи |
| grid-ui | Консоль |

Облачные права идут от **идентичности хоста** (AWS instance role / GCP ADC). Desired-state не хранит секреты. В проде — remote state, чтобы замена VM не теряла карту Terraform.

## Ваш desired state

**[grid-config](https://github.com/gridplatform/grid-config) — только пример.** Читайте его, чтобы понять форму JSON. **Не** форкайте для продакшена.

Для реального деплоя:

1. Создайте **новый** GitHub-репозиторий в своей org или аккаунте.
2. Добавьте свой path-shaped JSON (provider / env / resource units).
3. Укажите Grid на этот репозиторий (`GRID_GITOPS_REPO_URL`) — не на `grid-config`.

Копируйте паттерны из примера; репозиторий и настройки — ваши.

## Репозитории

| Repo | Роль |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Консоль |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | **Пример** desired-state (не ваш продовый fork) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Документация |

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
