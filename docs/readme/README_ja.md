<div align="center">

[English](../../profile/README.md) · [हिन्दी](README_hi.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · **日本語** · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### エンタープライズ向けのセルフホスト型インフラオーケストレーションプラットフォーム。

**企業がインフラを導入・運用するために — 主導権はあなたのもとへ。**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[クイックスタート](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [仕組み](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [あなたの desired state](https://github.com/gridplatform/grid-config#readme) · [リポジトリ](https://github.com/orgs/gridplatform/repositories) · [ドキュメント](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid は**セルフホスト**のクラウド基盤プラットフォームです。企業は展開の仕方、変更権限、アクセスの置き場所を自ら保ち、他社コンソールに主導権を渡さずに使えます。

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

Grid は、チームが**クラウド資源を依頼し**、**実際に何が変わったかを見る**場所です。

ネットワーク、サーバー、データベースなど、欲しいものを**あなた自身の** GitHub リポジトリの設定ファイルに書きます。Grid がその説明を読み、何が変わるかの計画を示し、あなたが承認すると、あなたのクラウド上で作成や削除を行います。変更は毎回、ライブログ付きのリリースとして残り、追ったり後から見返したりできます。

Grid は**あなたが**管理するマシンで動かします。クラウドへの権限はそのマシンの身分にあり — 設定ファイルにパスワードや鍵を入れる必要はありません。あとでマシンを替えても、Grid が管理しているものの記録は、一度用意したリモート保存先に残ります。

要するに：欲しいものを書き、計画を確認し、信頼できる履歴付きで適用する。

## あなたの desired state

**[grid-config](https://github.com/gridplatform/grid-config) はあくまで例です。** 設定の見た目を知るために使ってください。本番用に **fork しないでください**。

自分の環境では：

1. 自分の org / アカウントに **新しい** GitHub リポジトリを作る。
2. 自分の設定ファイルを置く（各環境で欲しいもの）。
3. Grid を**その**リポジトリに向ける — `grid-config` ではない。

例からアイデアを借り、リポジトリと設定は自分で所有する。

## リポジトリ

| リポジトリ | 何のためのものか |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | あなたのマシンで Grid を動かす仕組み — 裏側のエンジンとインストール方法 |
| [grid-ui](https://github.com/gridplatform/grid-ui) | ブラウザで使うウェブサイト |
| [grid-cli](https://github.com/gridplatform/grid-cli) | ウェブサイトを開かず、同じ作業をターミナルから行うツール |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | よく使うクラウド資源の既製パーツ（ネットワーク、サーバーなど） |
| [grid-config](https://github.com/gridplatform/grid-config) | 学び用のサンプル設定 — 本番のセットアップでは**ない**（自分のリポジトリを作る） |
| [grid-docs](https://github.com/gridplatform/grid-docs) | わかりやすいガイド |

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

[MIT](../../LICENSE) © 2026 Grid Platform。

各プロダクトリポジトリ（grid-core、grid-ui、grid-cli など）も同じ条件の `LICENSE` を持ちます。
