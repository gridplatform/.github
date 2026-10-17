<div align="center">

[English](../../profile/README.md) · [हिन्दी](README_hi.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · **ไทย** · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### แพลตฟอร์มจัดสรรโครงสร้างพื้นฐานแบบ self-host

**สร้างขึ้นให้องค์กรติดตั้งและจัดการโครงสร้างพื้นฐาน — โดยยังถือสิทธิ์ควบคุมไว้เอง**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://gridplatform.github.io/doc/)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://gridplatform.github.io/doc/) · [Status](../../STATUS.md)**

[เริ่มอย่างรวดเร็ว](https://gridplatform.github.io/doc/Install/VM) · [วิธีทำงาน](https://gridplatform.github.io/doc/Concepts/Overview) · [Desired state ของคุณ](https://github.com/gridplatform/grid-config#readme) · [Repositories](https://github.com/orgs/gridplatform/repositories) · [เอกสาร](https://gridplatform.github.io/doc/)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid เป็นแพลตฟอร์ม**self-host** สำหรับติดตั้งและเดินเครื่องโครงสร้างพื้นฐานคลาวด์ องค์กรใช้มันเพื่อคงไว้ซึ่งวิธีปล่อย ใครแก้ได้ และสิทธิ์เข้าถึงอยู่ที่ไหน — โดยไม่ยกการควบคุมนั้นให้คอนโซลของผู้ให้บริการรายอื่น

> **วิดีโอสาธิต** — เร็วๆ นี้

## เริ่มอย่างรวดเร็ว

1. สร้าง **[remote Terraform state](https://gridplatform.github.io/doc/Install/Remote_State)** (S3 / GCS / Azure)
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

เส้นทางเต็ม: **[ติดตั้งบน VM](https://gridplatform.github.io/doc/Install/VM)**

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
| [grid-docs](https://gridplatform.github.io/doc/) | คู่มือภาษาเข้าใจง่าย |

เสร็จ / กำลังทำ / วางแผน: **[STATUS.md](../../STATUS.md)**

## เอกสาร

| คู่มือ | ลิงก์ |
|-------|------|
| Org adoption | [organizations.md](https://gridplatform.github.io/doc/) |
| Remote state | [remote-state.md](https://gridplatform.github.io/doc/Install/Remote_State) |
| Install (VM / Compose) | [install/](https://gridplatform.github.io/doc/Install/Overview) |
| CLI (AWS / GCP) | [aws-gcp.md](https://gridplatform.github.io/doc/CLI/Overview) |
| Concepts | [concepts/overview.md](https://gridplatform.github.io/doc/Concepts/Overview) |

## การมีส่วนร่วม

Fork รีโป **ผลิตภัณฑ์** (core, ui, cli, terraform, docs) → สาขา → PR ไป `main`  
อย่าใช้ `grid-config` เป็นที่เก็บ desired-state ส่วนตัว

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues)

## สัญญาอนุญาต

[MIT](../../LICENSE) © 2026 Grid Platform

รีโปผลิตภัณฑ์ (grid-core, grid-ui, grid-cli ฯลฯ) มี `LICENSE` ของตนเองภายใต้เงื่อนไขเดียวกัน
