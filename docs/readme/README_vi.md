<div align="center">

[English](../../profile/README.md) · [हिन्दी](README_hi.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · **Tiếng Việt** · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### Nền tảng điều phối hạ tầng tự lưu trữ.

**Dành cho doanh nghiệp triển khai và quản lý hạ tầng — với quyền kiểm soát vẫn thuộc về bạn.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://gridplatform.github.io/doc/)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://gridplatform.github.io/doc/) · [Status](../../STATUS.md)**

[Bắt đầu nhanh](https://gridplatform.github.io/doc/Install/VM) · [Cách hoạt động](https://gridplatform.github.io/doc/Concepts/Overview) · [Desired state của bạn](https://github.com/gridplatform/grid-config#readme) · [Repositories](https://github.com/orgs/gridplatform/repositories) · [Tài liệu](https://gridplatform.github.io/doc/)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid là nền tảng **tự lưu trữ** để triển khai và vận hành hạ tầng đám mây. Doanh nghiệp dùng nó để giữ cách triển khai, ai được đổi, và nơi đặt quyền truy cập — mà không giao quyền đó cho bảng điều khiển của nhà cung cấp khác.

> **Video demo** — sắp ra mắt.

## Bắt đầu nhanh

1. Tạo **[remote Terraform state](https://gridplatform.github.io/doc/Install/Remote_State)** (S3 / GCS / Azure).
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

Đường đầy đủ: **[Cài trên VM](https://gridplatform.github.io/doc/Install/VM)**.

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

## Repositories

| Repository | Dùng để làm gì |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | Chạy Grid trên máy bạn — động cơ phía sau và cách cài đặt |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Trang web bạn dùng trong trình duyệt |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Cùng công việc từ dòng lệnh, không cần mở trang web |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Các khối sẵn cho tài nguyên đám mây phổ biến (mạng, máy chủ, …) |
| [grid-config](https://github.com/gridplatform/grid-config) | Cấu hình mẫu để học — **không** phải setup thật của bạn (hãy tạo repository riêng) |
| [grid-docs](https://gridplatform.github.io/doc/) | Hướng dẫn viết bằng lời dễ hiểu |

Xong / đang làm / kế hoạch: **[STATUS.md](../../STATUS.md)**.

## Tài liệu

| Hướng dẫn | Liên kết |
|-------|------|
| Org adoption | [organizations.md](https://gridplatform.github.io/doc/) |
| Remote state | [remote-state.md](https://gridplatform.github.io/doc/Install/Remote_State) |
| Install (VM / Compose) | [install/](https://gridplatform.github.io/doc/Install/Overview) |
| CLI (AWS / GCP) | [aws-gcp.md](https://gridplatform.github.io/doc/CLI/Overview) |
| Concepts | [concepts/overview.md](https://gridplatform.github.io/doc/Concepts/Overview) |

## Đóng góp

Fork repository **sản phẩm** (core, ui, cli, terraform, docs) → nhánh → PR vào `main`.  
Đừng coi `grid-config` là nhà desired-state riêng.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issues: [grid-core](https://github.com/gridplatform/grid-core/issues).

## Giấy phép

[MIT](../../LICENSE) © 2026 Grid Platform.

Các repository sản phẩm (grid-core, grid-ui, grid-cli, …) cũng có `LICENSE` riêng với cùng điều khoản.
