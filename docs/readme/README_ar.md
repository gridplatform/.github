<div align="center" dir="rtl">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · **العربية** · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### تنسيق بنية تحتية مستضافة ذاتيًا — JSON للحالة المرغوبة، وحدات Terraform، إصدارات قابلة للتدقيق.

**مستوى التحكم لديك. بيانات الاعتماد لديك. حالتك.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[بداية سريعة](#بداية-سريعة) · [كيف يعمل](#كيف-يعمل) · [حالتك المرغوبة](#حالتك-المرغوبة) · [المستودعات](#المستودعات) · [التوثيق](#التوثيق)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

يحوّل Grid بنية JSON ذات شكل مسار إلى Terraform عبر بنك وحدات عام، ويشغّل **plan / apply / destroy** كـ **releases** قابلة للتدقيق، ويوفّر وحدة تحكم بأسلوب GitOps. استضافة ذاتية على VM أو Docker Compose — بلا قفل مورّد، ومخرج عبر Terraform الصِرف.

> **فيديو تجريبي** — قريبًا.

## بداية سريعة

1. أنشئ **[حالة Terraform البعيدة](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. ثبّت Grid على VM (Compose افتراضيًا).

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

افتح `http://<host>/`. فضّل **دور المثيل / حساب الخدمة** على الـ VM بدل مفاتيح سحابية طويلة الأمد.

المسار الكامل: **[التثبيت على VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## كيف يعمل

| جزء | دور |
|-------|------|
| مستودع الحالة المرغوبة **الخاص بك** | مستودع GitHub **تنشئه أنت** — JSON لما تنشره |
| بنك الوحدات | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | واجهة API ومزامنة GitOps وإصدارات + سجلات مباشرة |
| grid-ui | وحدة التحكم |

صلاحيات السحابة تأتي من **هوية المضيف** (دور مثيل AWS / ADC لـ GCP). ملفات الحالة المرغوبة لا تحمل بيانات اعتماد. الإنتاج يستخدم حالة بعيدة حتى لا تفقد خريطة Terraform عند استبدال الـ VM.

## حالتك المرغوبة

**[grid-config](https://github.com/gridplatform/grid-config) مثال فقط.** اقرأه لتتعلم شكل JSON. **لا** تعمل له fork للإنتاج.

للنشر الحقيقي:

1. أنشئ مستودع GitHub **جديدًا** تحت منظمتك أو حسابك.
2. أضف JSON الخاص بك بشكل مسار (provider / env / وحدات الموارد).
3. وجّه Grid إلى ذلك المستودع (`GRID_GITOPS_REPO_URL`) — وليس إلى `grid-config`.

انسخ الأنماط من المثال؛ المستودع والإعدادات ملكك.

## المستودعات

| Repo | دور |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | وحدة التحكم |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | حالة مرغوبة **للمثال** (ليست fork إنتاجك) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | التوثيق |

منجز / قيد التنفيذ / مخطط: **[STATUS.md](../../STATUS.md)**.

## التوثيق

| دليل | رابط |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## المساهمة

اعمل fork لمستودع **منتج** (core، ui، cli، terraform، docs) → فرع → PR إلى `main`.  
لا تعامل `grid-config` كمنزل خاص لحالتك المرغوبة.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

المشكلات: [grid-core](https://github.com/gridplatform/grid-core/issues).

## الترخيص

MIT — see each repository’s `LICENSE`.
