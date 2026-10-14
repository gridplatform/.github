<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · **Bahasa Indonesia** · [Italiano](README_it.md)

# Grid Platform

### Orkestrasi infrastruktur self-hosted — JSON desired-state, modul Terraform, release yang diaudit.

**Control plane Anda. Kredensial Anda. State Anda.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Mulai cepat](#mulai-cepat) · [Cara kerja](#cara-kerja) · [Desired state Anda](#desired-state-anda) · [Repositori](#repositori) · [Dokumentasi](#dokumentasi)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid mengubah JSON infrastruktur berbentuk path menjadi Terraform lewat bank modul publik, menjalankan **plan / apply / destroy** sebagai **release** yang diaudit, dan menyediakan konsol bergaya GitOps. Self-host di VM atau Docker Compose — tanpa vendor lock-in, keluar lewat Terraform murni.

> **Video demo** — segera hadir.

## Mulai cepat

1. Buat **[remote Terraform state](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Pasang Grid di VM (default Compose).

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

Buka `http://<host>/`. Utamakan **instance role / service account** di VM daripada kunci cloud jangka panjang.

Jalur lengkap: **[Pasang di VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Cara kerja

| Bagian | Peran |
|-------|------|
| Repo desired-state **Anda** | Repo GitHub yang **Anda** buat — JSON yang Anda deploy |
| Bank modul | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, sinkron GitOps, release + log langsung |
| grid-ui | Konsol |

Izin cloud datang dari **identitas host** (AWS instance role / GCP ADC). File desired-state tidak membawa kredensial. Produksi memakai remote state agar VM pengganti tidak kehilangan peta Terraform.

## Desired state Anda

**[grid-config](https://github.com/gridplatform/grid-config) hanya contoh.** Baca untuk mempelajari bentuk JSON. **Jangan** fork untuk produksi.

Untuk deploy sungguhan:

1. Buat repositori GitHub **baru** di org atau akun Anda.
2. Tambahkan JSON berbentuk path milik Anda (provider / env / unit sumber daya).
3. Arahkan Grid ke repo itu (`GRID_GITOPS_REPO_URL`) — bukan ke `grid-config`.

Salin pola dari contoh; repo dan pengaturan milik Anda.

## Repositori

| Repo | Peran |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Konsol |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | Desired-state **contoh** (bukan fork produksi Anda) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Dokumentasi |

Selesai / berlangsung / direncanakan: **[STATUS.md](../../STATUS.md)**.

## Dokumentasi

| Panduan | Tautan |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Kontribusi

Fork repo **produk** (core, ui, cli, terraform, docs) → cabang → PR ke `main`.  
Jangan anggap `grid-config` sebagai rumah desired-state pribadi.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Lisensi

MIT — see each repository’s `LICENSE`.
