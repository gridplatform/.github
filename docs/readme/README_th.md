<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · **ไทย** · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### การจัดสรรโครงสร้างพื้นฐานแบบ self-host — JSON สถานะที่ต้องการ, โมดูล Terraform, release ที่ตรวจสอบได้

**คอนโทรลเพลนของคุณ ข้อมูลรับรองของคุณ สถานะของคุณ**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[เริ่มอย่างรวดเร็ว](#เริ่มอย่างรวดเร็ว) · [วิธีทำงาน](#วิธีทำงาน) · [Desired state ของคุณ](#desired-state-ของคุณ) · [รีโป](#รีโป) · [เอกสาร](#เอกสาร)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid แปลง JSON โครงสร้างพื้นฐานแบบ path เป็น Terraform ผ่านคลังโมดูลสาธารณะ รัน **plan / apply / destroy** เป็น **release** ที่ตรวจสอบได้ และมีคอนโซลแบบ GitOps Self-host บน VM หรือ Docker Compose — ไม่ล็อกผู้ให้บริการ ออกด้วย Terraform ล้วนได้

> **วิดีโอสาธิต** — เร็วๆ นี้

## เริ่มอย่างรวดเร็ว

1. สร้าง **[remote Terraform state](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure)
2. ติดตั้ง Grid บน VM (ค่าเริ่มต้น Compose)

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

เปิด `http://<host>/` ควรใช้ **instance role / service account** บน VM แทนคลาวด์คีย์ระยะยาว

เส้นทางเต็ม: **[ติดตั้งบน VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**

## วิธีทำงาน

| ส่วน | บทบาท |
|-------|------|
| รีโป desired-state **ของคุณ** | รีโป GitHub ที่ **คุณ** สร้าง — JSON ของสิ่งที่ deploy |
| คลังโมดูล | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, ซิงก์ GitOps, release + ล็อกสด |
| grid-ui | คอนโซล |

สิทธิ์คลาวด์มาจาก **ตัวตนของโฮสต์** (AWS instance role / GCP ADC) ไฟล์ desired-state ไม่พก credentials โปรดักชันใช้ remote state เพื่อไม่ให้เสียแผนที่ Terraform เมื่อเปลี่ยน VM

## Desired state ของคุณ

**[grid-config](https://github.com/gridplatform/grid-config) เป็นเพียงตัวอย่าง** อ่านเพื่อเรียนรู้รูปแบบ JSON **อย่า** fork สำหรับโปรดักชัน

สำหรับการ deploy จริง:

1. สร้างรีโป GitHub **ใหม่** ใต้ org หรือบัญชีของคุณ
2. เพิ่ม JSON แบบ path ของคุณเอง (provider / env / หน่วยทรัพยากร)
3. ชี้ Grid ไปที่รีโอนั้น (`GRID_GITOPS_REPO_URL`) — ไม่ใช่ `grid-config`

คัดลอกรูปแบบจากตัวอย่าง รีโปและการตั้งค่าเป็นของคุณ

## รีโป

| Repo | บทบาท |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | คอนโซล |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | desired-state **ตัวอย่าง** (ไม่ใช่ fork โปรดักชัน) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | เอกสาร |

เสร็จ / กำลังทำ / วางแผน: **[STATUS.md](../../STATUS.md)**

## เอกสาร

| คู่มือ | ลิงก์ |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## การมีส่วนร่วม

Fork รีโป **ผลิตภัณฑ์** (core, ui, cli, terraform, docs) → สาขา → PR ไป `main`  
อย่าใช้ `grid-config` เป็นที่เก็บ desired-state ส่วนตัว

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues)

## สัญญาอนุญาต

MIT — see each repository’s `LICENSE`.
