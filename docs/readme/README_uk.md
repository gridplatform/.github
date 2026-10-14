<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · **Українська** · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Self-hosted оркестрація інфраструктури — JSON бажаного стану, модулі Terraform, аудитовані релізи.

**Ваша control plane. Ваші облікові дані. Ваш стан.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Швидкий старт](#швидкий-старт) · [Як це працює](#як-це-працює) · [Ваш desired state](#ваш-desired-state) · [Репозиторії](#репозиторії) · [Документація](#документація)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid перетворює path-shaped JSON інфраструктури на Terraform через публічний банк модулів, виконує **plan / apply / destroy** як аудитовані **releases** і дає консоль у стилі GitOps. Self-host на VM або Docker Compose — без vendor lock-in, вихід через чистий Terraform.

> **Демо-відео** — незабаром.

## Швидкий старт

1. Створіть **[віддалений state Terraform](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Встановіть Grid на VM (за замовчуванням Compose).

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

Відкрийте `http://<host>/`. Краще **instance role / service account** на VM, ніж довгоживучі ключі.

Повний шлях: **[Встановлення на VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Як це працює

| Частина | Роль |
|-------|------|
| **Ваш** репозиторій desired-state | GitHub-репозиторій, який **створюєте ви** — JSON того, що деплоїте |
| Банк модулів | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, GitOps-синхронізація, релізи + live-логи |
| grid-ui | Консоль |

Хмарні права йдуть від **ідентичності хоста** (AWS instance role / GCP ADC). Desired-state не зберігає секрети. У проді — remote state, щоб заміна VM не губила карту Terraform.

## Ваш desired state

**[grid-config](https://github.com/gridplatform/grid-config) — лише приклад.** Читайте, щоб зрозуміти форму JSON. **Не** форкайте для продакшену.

Для реального деплою:

1. Створіть **новий** GitHub-репозиторій у своїй org або акаунті.
2. Додайте свій path-shaped JSON (provider / env / resource units).
3. Направте Grid на цей репозиторій (`GRID_GITOPS_REPO_URL`) — не на `grid-config`.

Копіюйте патерни з прикладу; репозиторій і налаштування — ваші.

## Репозиторії

| Repo | Роль |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Консоль |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | **Приклад** desired-state (не ваш продовий fork) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Документація |

Зроблено / в роботі / заплановано: **[STATUS.md](../../STATUS.md)**.

## Документація

| Гід | Посилання |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Участь

Форкніть **продуктовий** репозиторій (core, ui, cli, terraform, docs) → гілка → PR у `main`.  
Не використовуйте `grid-config` як особистий desired-state.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Ліцензія

MIT — see each repository’s `LICENSE`.
