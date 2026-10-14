<div align="center">

[English](../../profile/README.md) · [हिन्दी](README_hi.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · **Українська** · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Self-hosted платформа оркестрації інфраструктури.

**Для підприємств, які розгортають і керують інфраструктурою — з контролем, що лишається вашим.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Швидкий старт](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [Як це працює](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [Ваш desired state](https://github.com/gridplatform/grid-config#readme) · [Репозиторії](https://github.com/orgs/gridplatform/repositories) · [Документація](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid — це **self-hosted** платформа для розгортання й роботи хмарної інфраструктури. Підприємства використовують її, щоб зберігати, як усе викочується, хто може змінювати і де живе доступ — не віддаючи цей контроль чужій хмарній консолі.

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

Grid — місце, куди команда йде **попросити хмарні ресурси** і **побачити, що справді змінилось**.

Ви записуєте, що хочете — мережу, сервер, базу — у файлах конфігурації в GitHub-репозиторії, який **належить вам**. Grid читає цей опис, показує план змін і після вашого схвалення створює або видаляє ресурси у вашій хмарі. Кожна зміна зберігається як реліз із live-логами, щоб інші могли стежити й потім переглянути.

Ви запускаєте Grid на обладнанні під **вашим** контролем. Доступ до хмари лишається за ідентичністю цієї машини — у конфігах не потрібні паролі чи ключі. Якщо машину потім замінять, запис про те, чим керує Grid, лишиться у віддаленому сховищі, яке ви один раз налаштували.

Коротко: скажіть, що потрібно, перевірте план, застосуйте з історією, якій можна довіряти.

## Ваш desired state

**[grid-config](https://github.com/gridplatform/grid-config) — лише приклад.** Дивіться, як виглядають конфіги. **Не** форкайте для реального середовища.

Для свого setup:

1. Створіть **новий** GitHub-репозиторій у своїй org або акаунті.
2. Покладіть туди свої файли конфігурації (що потрібно в кожному середовищі).
3. Направте Grid на **цей** репозиторій — не на `grid-config`.

Беріть ідеї з прикладу; володіння репозиторієм і налаштуваннями залишайте собі.

## Репозиторії

| Репозиторій | Для чого це |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Запускає Grid на вашій машині — рушій за лаштунками та спосіб встановлення |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Сайт, яким ви користуєтесь у браузері |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Та сама робота з терміналу, без відкриття сайту |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Готові блоки для звичайних хмарних ресурсів (мережі, сервери тощо) |
| [grid-config](https://github.com/gridplatform/grid-config) | Приклад конфігів для навчання — **не** ваш реальний setup (створіть власний репозиторій) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Посібники простою мовою |

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

[MIT](../../LICENSE) © 2026 Grid Platform.

Продуктові репозиторії (grid-core, grid-ui, grid-cli тощо) мають власні `LICENSE` на тих самих умовах.
