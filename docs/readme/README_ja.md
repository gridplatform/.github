<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · **日本語** · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### セルフホストのインフラオーケストレーション — 望ましい状態の JSON、Terraform モジュール、監査可能なリリース。

**あなたのコントロールプレーン。あなたの認証情報。あなたの状態。**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[クイックスタート](#クイックスタート) · [仕組み](#仕組み) · [あなたの desired state](#あなたの-desired-state) · [リポジトリ](#リポジトリ) · [ドキュメント](#ドキュメント)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid はパス形式のインフラ JSON を公開モジュールバンク経由で Terraform に変換し、監査可能な **release** として **plan / apply / destroy** を実行し、GitOps スタイルのコンソールを提供します。VM または Docker Compose でセルフホスト — ベンダーロックインなし、素の Terraform で退出可能。

> **デモ動画** — 近日公開。

## クイックスタート

1. **[リモート Terraform 状態](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** を作成（S3 / GCS / Azure）。
2. VM に Grid をインストール（既定は Compose）。

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

`http://<host>/` を開く。長期のクラウドキーより VM の **インスタンスロール / サービスアカウント** を優先。

詳細：**[VM へのインストール](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**。

## 仕組み

| 要素 | 役割 |
|-------|------|
| **あなたの** desired-state リポジトリ | あなたが作る GitHub リポジトリ — デプロイ内容の JSON |
| モジュールバンク | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API、GitOps 同期、リリース + ライブログ |
| grid-ui | コンソール |

クラウド権限は **ホストの ID**（AWS インスタンスロール / GCP ADC）から来ます。desired-state に認証情報は含めません。本番はリモート状態を使い、VM を置き換えても Terraform の対応関係を失いません。

## あなたの desired state

**[grid-config](https://github.com/gridplatform/grid-config) はあくまで例です。** JSON の形を学ぶために読んでください。本番用に **fork しないでください**。

本番デプロイでは：

1. 自分の org / アカウントに **新しい** GitHub リポジトリを作る。
2. 自分のパス形式 JSON を追加する（provider / env / リソース単位）。
3. Grid をそのリポジトリに向ける（`GRID_GITOPS_REPO_URL`）— `grid-config` ではない。

例からパターンをコピーし、リポジトリと設定は自分で所有する。

## リポジトリ

| Repo | 役割 |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | コンソール |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | **例**の desired-state（本番の fork ではない） |
| [grid-docs](https://github.com/gridplatform/grid-docs) | ドキュメント |

完了 / 進行中 / 予定：**[STATUS.md](../../STATUS.md)**。

## ドキュメント

| ガイド | リンク |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## コントリビュート

**プロダクト**リポジトリ（core、ui、cli、terraform、docs）を fork → ブランチ → `main` へ PR。  
`grid-config` を私有の desired-state 置き場にしないでください。

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

Issue：[grid-core](https://github.com/gridplatform/grid-core/issues)。

## ライセンス

MIT — see each repository’s `LICENSE`.
