<div align="center" dir="rtl">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · **العربية** · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### منصة تنسيق البنية التحتية المستضافة ذاتيًا.

**مبنية للمؤسسات لنشر البنية التحتية وإدارتها — مع سيطرة تبقى لكم.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[بداية سريعة](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [كيف يعمل](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [حالتك المرغوبة](https://github.com/gridplatform/grid-config#readme) · [المستودعات](https://github.com/orgs/gridplatform/repositories) · [التوثيق](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid منصة **مستضافة ذاتيًا** لنشر وتشغيل البنية التحتية السحابية. تستخدمها المؤسسات للإبقاء على كيفية النشر ومن يغيّر وأين يعيش الوصول — دون تسليم تلك السيطرة لوحة تحكم مورّد آخر.

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

Grid هو المكان الذي تذهب إليه فرقك **لطلب موارد سحابية** و**رؤية ما تغيّر فعلًا**.

تكتب ما تريده — شبكةً أو خادمًا أو قاعدة بيانات — في ملفات إعداد داخل مستودع GitHub **تملكه**. يقرأ Grid هذا الوصف ويعرض خطة ما سيتغيّر، وعندما توافق ينشئ تلك الموارد أو يحذفها في سحابتك. يُحفظ كل تغيير كإصدار مع سجلات مباشرة ليتابع الآخرون ويعودوا لاحقًا.

تشغّل Grid على عتاد تحت سيطرة **ك**. يبقى الوصول السحابي مع هوية ذلك الجهاز — ولا تحتاج ملفات الإعداد إلى كلمات مرور أو مفاتيح بداخلها. إذا استُبدل الجهاز لاحقًا، يبقى سجل ما يديره Grid في التخزين البعيد الذي أعددته مرة واحدة.

باختصار: قل ما تريد، راجع الخطة، طبّق بمسار يمكن الوثوق به.

## حالتك المرغوبة

**[grid-config](https://github.com/gridplatform/grid-config) مثال فقط.** استخدمه لترى شكل الإعدادات. **لا** تعمل له fork لبيئتك الحقيقية.

لإعدادك أنت:

1. أنشئ مستودع GitHub **جديدًا** تحت منظمتك أو حسابك.
2. ضع ملفات الإعداد الخاصة بك هناك (ما تريده في كل بيئة).
3. وجّه Grid إلى **ذلك** المستودع — وليس إلى `grid-config`.

استعر أفكارًا من المثال؛ احتفظ بملكية المستودع والإعدادات.

## المستودعات

| المستودع | الغرض منه |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | يشغّل Grid على جهازك — المحرك من وراء الكواليس وطريقة التثبيت |
| [grid-ui](https://github.com/gridplatform/grid-ui) | الموقع الذي تستخدمه في المتصفح |
| [grid-cli](https://github.com/gridplatform/grid-cli) | نفس العمل من سطر الأوامر دون فتح الموقع |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | قطع جاهزة لموارد سحابية شائعة (شبكات وخوادم وغيرها) |
| [grid-config](https://github.com/gridplatform/grid-config) | إعدادات نموذجية للتعلّم — **ليست** إعدادك الحقيقي (أنشئ مستودعك الخاص) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | أدلة بلغة واضحة |

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
