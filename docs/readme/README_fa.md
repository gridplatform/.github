<div align="center" dir="rtl">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · **فارسی** · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### ارکستراسیون زیرساخت خودمیزبان — JSON وضعیت مطلوب، ماژول‌های Terraform، انتشارهای قابل‌ممیزی.

**صفحه کنترل شما. اعتبارنامه‌های شما. وضعیت شما.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[شروع سریع](#شروع-سریع) · [نحوه کار](#نحوه-کار) · [Desired state شما](#desired-state-شما) · [مخازن](#مخازن) · [مستندات](#مستندات)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid JSON زیرساخت مسیرشکل را از طریق بانک ماژول عمومی به Terraform تبدیل می‌کند، **plan / apply / destroy** را به‌صورت **release** قابل‌ممیزی اجرا می‌کند و کنسول سبک GitOps ارائه می‌دهد. روی VM یا Docker Compose خودمیزبان کنید — بدون قفل فروشنده، خروج با Terraform خالص.

> **ویدیوی دمو** — به‌زودی.

## شروع سریع

1. **[وضعیت دور Terraform](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** بسازید (S3 / GCS / Azure).
2. Grid را روی VM نصب کنید (پیش‌فرض Compose).

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

`http://<host>/` را باز کنید. **نقش نمونه / حساب سرویس** روی VM را به کلیدهای ابری بلندمدت ترجیح دهید.

مسیر کامل: **[نصب روی VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## نحوه کار

| بخش | نقش |
|-------|------|
| مخزن desired-state **شما** | مخزن GitHub که **خودتان** می‌سازید — JSON آنچه دیپلوی می‌کنید |
| بانک ماژول | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API، همگام‌سازی GitOps، انتشار + لاگ زنده |
| grid-ui | کنسول |

مجوزهای ابری از **هویت میزبان** می‌آید (نقش نمونه AWS / ADC جی‌سی‌پی). فایل‌های desired-state اعتبارنامه ندارند. تولید از وضعیت دور استفاده می‌کند تا با تعویض VM نقشه Terraform از دست نرود.

## Desired state شما

**[grid-config](https://github.com/gridplatform/grid-config) فقط یک مثال است.** برای یادگیری شکل JSON بخوانید. برای تولید **فورک نکنید**.

برای دیپلوی واقعی:

1. یک مخزن GitHub **جدید** زیر سازمان یا حسابتان بسازید.
2. JSON مسیرشکل خود را اضافه کنید (provider / env / واحدهای منبع).
3. Grid را به آن مخزن اشاره دهید (`GRID_GITOPS_REPO_URL`) — نه به `grid-config`.

الگوها را از مثال کپی کنید؛ مخزن و تنظیمات مال شماست.

## مخازن

| Repo | نقش |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | کنسول |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | desired-state **نمونه** (نه فورک تولید شما) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | مستندات |

انجام‌شده / در حال انجام / برنامه‌ریزی‌شده: **[STATUS.md](../../STATUS.md)**.

## مستندات

| راهنما | پیوند |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## مشارکت

یک مخزن **محصول** را فورک کنید (core، ui، cli، terraform، docs) → شاخه → PR به `main`.  
`grid-config` را خانهٔ خصوصی desired-state خود ندانید.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## مجوز

MIT — see each repository’s `LICENSE`.
