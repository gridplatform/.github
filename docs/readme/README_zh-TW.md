<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · **繁體中文** · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### 自託管基礎建設編排 — 期望狀態 JSON、Terraform 模組、可稽核發布。

**你的控制平面。你的憑證。你的狀態。**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[快速開始](#快速開始) · [運作方式](#運作方式) · [你的期望狀態](#你的期望狀態) · [倉庫](#倉庫) · [文件](#文件)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid 將路徑形基礎建設 JSON 透過公共模組庫轉為 Terraform，以可稽核的 **release** 執行 **plan / apply / destroy**，並提供 GitOps 風格控制台。在 VM 或 Docker Compose 上自託管 — 無廠商鎖定，可走純 Terraform 退出路徑。

> **示範影片** — 即將推出。

## 快速開始

1. 建立 **[遠端 Terraform 狀態](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)**（S3 / GCS / Azure）。
2. 在 VM 上安裝 Grid（預設 Compose）。

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

開啟 `http://<host>/`。優先使用 VM 上的 **執行個體角色 / 服務帳戶**，避免長期雲端金鑰。

完整步驟：**[在 VM 上安裝](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**。

## 運作方式

| 元件 | 用途 |
|-------|------|
| **你的**期望狀態倉庫 | 你自己建立的 GitHub 倉庫 — 存放要部署的 JSON |
| 模組庫 | Terraform 模組（[grid-terraform](https://github.com/gridplatform/grid-terraform)） |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API、GitOps 同步、release + 即時日誌 |
| grid-ui | 主控台 |

雲端權限來自 **主機身分**（AWS 執行個體角色 / GCP ADC）。期望狀態檔案不攜帶憑證。正式環境使用遠端狀態，更換 VM 也不會遺失 Terraform 對應。

## 你的期望狀態

**[grid-config](https://github.com/gridplatform/grid-config) 僅供範例。** 閱讀它以了解 JSON 結構。**不要**為正式環境 fork 它。

對於真實部署：

1. 在你的組織或帳號下 **新建** GitHub 倉庫。
2. 加入你自己的路徑形 JSON（provider / env / 資源單元）。
3. 讓 Grid 指向該倉庫（`GRID_GITOPS_REPO_URL`）— 而不是 `grid-config`。

從範例複製模式；倉庫與設定歸你所有。

## 倉庫

| 倉庫 | 用途 |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | 主控台 |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform 模組（[grid-terraform](https://github.com/gridplatform/grid-terraform)） |
| [grid-config](https://github.com/gridplatform/grid-config) | **範例**期望狀態（不是你的正式 fork） |
| [grid-docs](https://github.com/gridplatform/grid-docs) | 文件 |

完成 / 進行中 / 計劃：**[STATUS.md](../../STATUS.md)**。

## 文件

| 指南 | 連結 |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## 貢獻

Fork **產品**倉庫（core、ui、cli、terraform、docs）→ 分支 → 向 `main` 提 PR。  
不要把 `grid-config` 當作你的私有期望狀態倉庫。

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

問題回報：[grid-core](https://github.com/gridplatform/grid-core/issues)。

## 授權

MIT — 見各倉庫的 `LICENSE`。
