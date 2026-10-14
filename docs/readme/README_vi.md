<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · **Tiếng Việt** · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Điều phối hạ tầng tự lưu trữ — JSON trạng thái mong muốn, module Terraform, release có kiểm toán.

**Control plane của bạn. Thông tin xác thực của bạn. State của bạn.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[Bắt đầu nhanh](#bắt-đầu-nhanh) · [Cách hoạt động](#cách-hoạt-động) · [Desired state của bạn](#desired-state-của-bạn) · [Kho mã](#kho-mã) · [Tài liệu](#tài-liệu)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid giúp bạn **tự yêu cầu, xem lại và chạy hạ tầng đám mây** — không khóa setup vào sản phẩm của người khác. Bạn mô tả điều muốn có, duyệt thay đổi với lịch sử rõ ràng, và giữ quyền truy cập cùng hồ sơ trên máy móc và lưu trữ do **bạn** kiểm soát.

> **Video demo** — sắp ra mắt.

## Bắt đầu nhanh

1. Tạo **[remote Terraform state](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** (S3 / GCS / Azure).
2. Cài Grid trên VM (mặc định Compose).

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

Mở `http://<host>/`. Ưu tiên **instance role / service account** trên VM thay vì khóa cloud dài hạn.

Đường đầy đủ: **[Cài trên VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## Cách hoạt động

Grid là nơi nhóm bạn **xin tài nguyên đám mây** và **xem thực sự đã thay đổi gì**.

Bạn viết những gì muốn — mạng, máy chủ, cơ sở dữ liệu — vào các tệp cấu hình trong repository GitHub do **bạn** sở hữu. Grid đọc mô tả đó, hiện kế hoạch những gì sẽ đổi, và khi bạn duyệt thì tạo hoặc xóa các tài nguyên đó trên đám mây của bạn. Mọi thay đổi được lưu thành một release kèm log trực tiếp để người khác theo dõi và xem lại sau.

Bạn chạy Grid trên phần cứng do **bạn** kiểm soát. Quyền truy cập đám mây gắn với danh tính máy đó — tệp cấu hình không cần mật khẩu hay khóa bên trong. Nếu sau này thay máy, hồ sơ về những gì Grid quản lý vẫn nằm ở kho lưu trữ từ xa bạn đã thiết lập một lần.

Tóm lại: nói rõ bạn muốn gì, xem kế hoạch, áp dụng với dấu vết đáng tin.

## Desired state của bạn

**[grid-config](https://github.com/gridplatform/grid-config) chỉ là ví dụ.** Dùng để xem cấu hình trông thế nào. **Không** fork cho môi trường thật.

Cho setup của bạn:

1. Tạo repository GitHub **mới** dưới org hoặc tài khoản của bạn.
2. Đặt các tệp cấu hình của bạn vào đó (muốn gì ở mỗi môi trường).
3. Trỏ Grid tới **repository đó** — không phải `grid-config`.

Mượn ý từ ví dụ; giữ quyền sở hữu repository và cài đặt.

## Kho mã

| Repository | Vai trò |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Console |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | Desired-state **ví dụ** (không phải fork production) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Tài liệu |

Xong / đang làm / kế hoạch: **[STATUS.md](../../STATUS.md)**.

## Tài liệu

| Hướng dẫn | Liên kết |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## Đóng góp

Fork repository **sản phẩm** (core, ui, cli, terraform, docs) → nhánh → PR vào `main`.  
Đừng coi `grid-config` là nhà desired-state riêng.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Giấy phép

MIT — see each repository’s `LICENSE`.
