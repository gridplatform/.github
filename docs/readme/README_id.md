<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · **Bahasa Indonesia** · [Italiano](README_it.md)

# Grid Platform

### Platform orkestrasi infrastruktur self-hosted.

**Dibangun agar perusahaan dapat men-deploy dan mengelola infrastruktur — dengan kontrol yang tetap milik Anda.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Mulai cepat](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [Cara kerja](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [Desired state Anda](https://github.com/gridplatform/grid-config#readme) · [Repositori](https://github.com/orgs/gridplatform/repositories) · [Dokumentasi](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid adalah platform **self-hosted** untuk men-deploy dan menjalankan infrastruktur cloud. Perusahaan menggunakannya agar cara rilis, siapa yang boleh mengubah, dan di mana akses berada tetap di tangan mereka — tanpa menyerahkan kontrol itu ke konsol vendor lain.

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

Grid adalah tempat tim Anda **meminta sumber daya cloud** dan **melihat apa yang benar-benar berubah**.

Anda menuliskan apa yang diinginkan — jaringan, server, basis data — dalam file konfigurasi di repository GitHub yang **Anda** miliki. Grid membaca deskripsi itu, menampilkan rencana perubahan, dan saat Anda setujui, membuat atau menghapus sumber daya itu di cloud Anda. Setiap perubahan disimpan sebagai release dengan log langsung agar orang lain bisa mengikuti dan melihat lagi nanti.

Anda menjalankan Grid di perangkat keras di bawah kendali **Anda**. Akses cloud tetap pada identitas mesin itu — file konfigurasi tidak perlu memuat kata sandi atau kunci. Jika mesin diganti nanti, catatan tentang apa yang dikelola Grid tetap ada di penyimpanan jarak jauh yang Anda siapkan sekali.

Singkatnya: katakan apa yang Anda mau, tinjau rencana, terapkan dengan jejak yang bisa dipercaya.

## Desired state Anda

**[grid-config](https://github.com/gridplatform/grid-config) hanya contoh.** Gunakan untuk melihat bentuk konfigurasi. **Jangan** fork untuk lingkungan nyata Anda.

Untuk setup Anda sendiri:

1. Buat repositori GitHub **baru** di org atau akun Anda.
2. Taruh file konfigurasi Anda sendiri di sana (apa yang Anda inginkan di tiap lingkungan).
3. Arahkan Grid ke **repository itu** — bukan ke `grid-config`.

Pinjam ide dari contoh; tetap miliki repository dan pengaturannya.

## Repositori

| Repositori | Untuk apa |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Menjalankan Grid di mesin Anda — mesin di balik layar plus cara memasangnya |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Situs web yang Anda pakai di browser |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Pekerjaan yang sama dari terminal, tanpa membuka situs |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Bagian siap pakai untuk sumber daya cloud umum (jaringan, server, dan lainnya) |
| [grid-config](https://github.com/gridplatform/grid-config) | Contoh konfigurasi untuk belajar — **bukan** setup nyata Anda (buat repositori sendiri) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Panduan dalam bahasa yang jelas |

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

Fork repository **produk** (core, ui, cli, terraform, docs) → cabang → PR ke `main`.  
Jangan anggap `grid-config` sebagai rumah desired-state pribadi.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Lisensi

MIT — see each repository’s `LICENSE`.
