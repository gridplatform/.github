<div align="center" dir="rtl">

[English](../../profile/README.md) · [हिन्दी](README_hi.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · **فارسی** · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### پلتفرم ارکستراسیون زیرساخت خودمیزبان.

**برای سازمان‌هایی که زیرساخت را مستقر و مدیریت می‌کنند — با کنترلی که مال شما می‌ماند.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://gridplatform.github.io/doc/)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://gridplatform.github.io/doc/) · [Status](../../STATUS.md)**

[شروع سریع](https://gridplatform.github.io/doc/Install/VM) · [نحوه کار](https://gridplatform.github.io/doc/Concepts/Overview) · [Desired state شما](https://github.com/gridplatform/grid-config#readme) · [مخازن](https://github.com/orgs/gridplatform/repositories) · [مستندات](https://gridplatform.github.io/doc/)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid یک پلتفرم **خودمیزبان** برای استقرار و اجرای زیرساخت ابری است. سازمان‌ها با آن نحوهٔ انتشار، اینکه چه کسی می‌تواند تغییر دهد و دسترسی کجا می‌ماند را نزد خود نگه می‌دارند — بدون سپردن آن کنترل به کنسول فروشندهٔ دیگر.

> **ویدیوی دمو** — به‌زودی.

## شروع سریع

1. **[وضعیت دور Terraform](https://gridplatform.github.io/doc/Install/Remote_State)** بسازید (S3 / GCS / Azure).
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

مسیر کامل: **[نصب روی VM](https://gridplatform.github.io/doc/Install/VM)**.

## نحوه کار

Grid جایی است که تیمتان برای **درخواست منابع ابری** و **دیدن اینکه واقعاً چه عوض شده** می‌رود.

آنچه می‌خواهید — شبکه، سرور، پایگاه‌داده — را در فایل‌های پیکربندی در مخزن GitHub متعلق به **خودتان** می‌نویسید. Grid آن توصیف را می‌خواند، برنامه‌ای از تغییرات نشان می‌دهد و با تأیید شما آن منابع را در ابرتان می‌سازد یا حذف می‌کند. هر تغییر به‌صورت release با لاگ زنده ذخیره می‌شود تا دیگران دنبال کنند و بعداً برگردند.

Grid را روی سخت‌افزاری زیر کنترل **خودتان** اجرا می‌کنید. دسترسی ابری با هویت همان ماشین می‌ماند — فایل‌های پیکربندی نیازی به رمز یا کلید داخلشان ندارند. اگر بعداً ماشین عوض شود، سابقهٔ آنچه Grid مدیریت می‌کند در ذخیرهٔ دوری که یک‌بار راه‌اندازی کردید می‌ماند.

خلاصه: بگویید چه می‌خواهید، برنامه را مرور کنید، با ردپایی قابل اعتماد اعمال کنید.

## Desired state شما

**[grid-config](https://github.com/gridplatform/grid-config) فقط یک مثال است.** برای دیدن شکل پیکربندی‌ها از آن استفاده کنید. برای محیط واقعی **فورک نکنید**.

برای setup خودتان:

1. یک مخزن GitHub **جدید** زیر سازمان یا حسابتان بسازید.
2. فایل‌های پیکربندی خود را آنجا بگذارید (در هر محیط چه می‌خواهید).
3. Grid را به **آن** مخزن اشاره دهید — نه به `grid-config`.

از مثال ایده بگیرید؛ مالکیت مخزن و تنظیمات را برای خود نگه دارید.

## مخازن

| مخزن | برای چیست |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Grid را روی ماشین شما اجرا می‌کند — موتور پشت‌صحنه و نحوه نصب |
| [grid-ui](https://github.com/gridplatform/grid-ui) | وب‌سایتی که در مرورگر استفاده می‌کنید |
| [grid-cli](https://github.com/gridplatform/grid-cli) | همان کار از ترمینال، بدون باز کردن وب‌سایت |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | قطعات آماده برای منابع ابری رایج (شبکه، سرور و بیشتر) |
| [grid-config](https://github.com/gridplatform/grid-config) | پیکربندی نمونه برای یادگیری — setup واقعی شما **نیست** (مخزن خودتان را بسازید) |
| [grid-docs](https://gridplatform.github.io/doc/) | راهنماها به زبان ساده |

انجام‌شده / در حال انجام / برنامه‌ریزی‌شده: **[STATUS.md](../../STATUS.md)**.

## مستندات

| راهنما | پیوند |
|-------|------|
| Org adoption | [organizations.md](https://gridplatform.github.io/doc/) |
| Remote state | [remote-state.md](https://gridplatform.github.io/doc/Install/Remote_State) |
| Install (VM / Compose) | [install/](https://gridplatform.github.io/doc/Install/Overview) |
| CLI (AWS / GCP) | [aws-gcp.md](https://gridplatform.github.io/doc/CLI/Overview) |
| Concepts | [concepts/overview.md](https://gridplatform.github.io/doc/Concepts/Overview) |

## مشارکت

یک مخزن **محصول** را فورک کنید (core، ui، cli، terraform، docs) → شاخه → PR به `main`.  
`grid-config` را خانهٔ خصوصی desired-state خود ندانید.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## مجوز

[MIT](../../LICENSE) © 2026 Grid Platform.

مخازن محصول (grid-core، grid-ui، grid-cli و بقیه) نیز `LICENSE` خود را با همان شرایط دارند.
