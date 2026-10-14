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

Grid ช่วยให้คุณ**ขอ ตรวจทาน และรันโครงสร้างพื้นฐานคลาวด์ด้วยตัวเอง** — โดยไม่ล็อก setup ไว้ในผลิตภัณฑ์ของคนอื่น คุณบอกว่าต้องการอะไร อนุมัติการเปลี่ยนแปลงพร้อมประวัติชัดเจน และเก็บสิทธิ์เข้าถึงกับบันทึกไว้บนเครื่องและที่เก็บภายใต้การควบคุมของ**คุณ**

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

Grid คือที่ที่ทีมของคุณไป**ขอทรัพยากรคลาวด์**และ**ดูว่าอะไรเปลี่ยนจริงๆ**

คุณเขียนสิ่งที่ต้องการ — เครือข่าย เซิร์ฟเวอร์ ฐานข้อมูล — ในไฟล์คอนฟิกในรีโป GitHub ที่**คุณ**เป็นเจ้าของ Grid อ่านคำอธิบายนั้น แสดงแผนว่าอะไรจะเปลี่ยน และเมื่อคุณอนุมัติก็สร้างหรือลบทรัพยากรเหล่านั้นในคลาวด์ของคุณ ทุกการเปลี่ยนแปลงถูกบันทึกเป็น release พร้อมล็อกสด ให้คนอื่นตามดูและย้อนดูภายหลังได้

คุณรัน Grid บนฮาร์ดแวร์ที่**คุณ**ควบคุม การเข้าถึงคลาวด์อยู่กับตัวตนของเครื่องนั้น — ไฟล์คอนฟิกไม่ต้องมีรหัสผ่านหรือคีย์อยู่ข้างใน หากเปลี่ยนเครื่องภายหลัง บันทึกว่า Grid จัดการอะไรอยู่ยังอยู่ในที่เก็บระยะไกลที่คุณตั้งไว้ครั้งเดียว

สรุป: บอกว่าต้องการอะไร ตรวจแผน แล้วใช้กับร่องรอยที่ไว้ใจได้

## Desired state ของคุณ

**[grid-config](https://github.com/gridplatform/grid-config) เป็นเพียงตัวอย่าง** ใช้ดูว่าคอนฟิกหน้าตาเป็นอย่างไร **อย่า** fork สำหรับสภาพแวดล้อมจริง

สำหรับ setup ของคุณ:

1. สร้างรีโป GitHub **ใหม่** ใต้ org หรือบัญชีของคุณ
2. ใส่ไฟล์คอนฟิกของคุณเอง (ต้องการอะไรในแต่ละสภาพแวดล้อม)
3. ชี้ Grid ไปที่**รีโอนั้น** — ไม่ใช่ `grid-config`

ยืมไอเดียจากตัวอย่าง เก็บความเป็นเจ้าของรีโปและการตั้งค่าไว้เอง

## Repositories

| Repository | มีไว้ทำอะไร |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | รัน Grid บนเครื่องคุณ — เอนจินเบื้องหลังและวิธีติดตั้ง |
| [grid-ui](https://github.com/gridplatform/grid-ui) | เว็บไซต์ที่คุณใช้ในเบราว์เซอร์ |
| [grid-cli](https://github.com/gridplatform/grid-cli) | งานเดียวกันจากเทอร์มินัล โดยไม่ต้องเปิดเว็บไซต์ |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | ชิ้นส่วนพร้อมใช้สำหรับทรัพยากรคลาวด์ทั่วไป (เครือข่าย เซิร์ฟเวอร์ และอื่นๆ) |
| [grid-config](https://github.com/gridplatform/grid-config) | คอนฟิกตัวอย่างสำหรับเรียนรู้ — **ไม่ใช่** setup จริงของคุณ (สร้าง repository ของคุณเอง) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | คู่มือภาษาเข้าใจง่าย |

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
