<div align="center">

[English](../../profile/README.md) · [हिन्दी](README_hi.md) · [简体中文](README_zh.md) · **繁體中文** · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### 企業可用的自託管基礎建設編排平台。

**為企業部署與管理基礎建設而建 — 控制權留在你手中。**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[快速開始](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [運作方式](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [你的期望狀態](https://github.com/gridplatform/grid-config#readme) · [倉庫](https://github.com/orgs/gridplatform/repositories) · [文件](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid 是一套**自託管**的雲端基礎建設部署與運行平台。企業用它掌握如何上線、誰能改、存取落在哪裡 — 而不必把控制權交給別家廠商的主控台。

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

Grid 是團隊用來**申請雲端資源**並**看清楚實際改了什麼**的地方。

你把想要的東西寫下來 — 網路、伺服器、資料庫 — 放進**你自己**的 GitHub 倉庫裡的設定檔。Grid 讀取這些描述，顯示一份會改動什麼的計畫；你核准後，就在你的雲端建立或移除這些資源。每次變更都存成帶即時日誌的發布紀錄，別人可以跟著看，也可以事後回看。

你在**自己**控制的機器上執行 Grid。雲端存取權限留在那台機器的身分上 — 設定檔裡不需要密碼或金鑰。如果之後換了機器，Grid 管理過什麼的紀錄仍留在你當初設好的遠端儲存裡。

一句話：說出你要什麼，審閱計畫，帶著可信的軌跡去執行。

## 你的期望狀態

**[grid-config](https://github.com/gridplatform/grid-config) 僅供範例。** 用它了解設定長什麼樣子。**不要**為真實環境 fork 它。

你自己的用法：

1. 在你的組織或帳號下 **新建** GitHub 倉庫。
2. 放入你自己的設定檔（每個環境想要什麼）。
3. 讓 Grid 指向**那個**倉庫 — 而不是 `grid-config`。

可以從範例借鏡想法；倉庫與設定歸你所有。

## 倉庫

| 倉庫 | 用途 |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | 在你的機器上執行 Grid — 背後的引擎，以及如何安裝 |
| [grid-ui](https://github.com/gridplatform/grid-ui) | 你在瀏覽器裡用的網站 |
| [grid-cli](https://github.com/gridplatform/grid-cli) | 同樣的工作，在終端機完成，不必開啟網站 |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | 常見雲端資源的現成積木（網路、伺服器等） |
| [grid-config](https://github.com/gridplatform/grid-config) | 用來學習的範例設定 — **不是**你的真實環境（請自建倉庫） |
| [grid-docs](https://github.com/gridplatform/grid-docs) | 淺白易懂的指南 |

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

[MIT](../../LICENSE) © 2026 Grid Platform。

各產品倉庫（grid-core、grid-ui、grid-cli 等）在相同條款下各自帶有 `LICENSE`。
