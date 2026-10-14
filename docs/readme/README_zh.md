<div align="center">

[English](../../profile/README.md) · [हिन्दी](README_hi.md) · **简体中文** · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### 企业可用的自托管基础设施编排平台。

**为企业部署与管理基础设施而建 — 控制权留在你手中。**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](../../LICENSE)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[快速开始](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md) · [工作原理](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) · [你的期望状态](https://github.com/gridplatform/grid-config#readme) · [仓库](https://github.com/orgs/gridplatform/repositories) · [文档](https://github.com/gridplatform/grid-docs)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid 是一套**自托管**的云基础设施部署与运行平台。企业用它掌握如何上线、谁能改、访问落在哪里 — 而不必把控制权交给别家厂商的控制台。

> **演示视频** — 即将推出。

## 快速开始

1. 创建 **[远程 Terraform 状态](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)**（S3 / GCS / Azure）。
2. 在 VM 上安装 Grid（默认 Compose）。

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

打开 `http://<host>/`。优先使用 VM 上的 **实例角色 / 服务账号**，避免长期云密钥。

完整步骤：**[在 VM 上安装](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**。

## 工作原理

Grid 是团队用来**申请云资源**并**看清实际改了什么**的地方。

你把想要的东西写下来 — 网络、服务器、数据库 — 放进**你自己**的 GitHub 仓库里的配置文件。Grid 读取这些描述，展示一份会改动什么的计划；你批准后，就在你的云里创建或删除这些资源。每次变更都保存为带实时日志的发布记录，别人可以跟着看，也可以事后回看。

你在**自己**控制的机器上运行 Grid。云访问权限留在那台机器的身份上 — 配置文件里不需要密码或密钥。如果以后换了机器，Grid 管理过什么的记录仍留在你当初设好的远程存储里。

一句话：说出你要什么，审阅计划，带着可信的轨迹去执行。

## 你的期望状态

**[grid-config](https://github.com/gridplatform/grid-config) 仅作示例。** 用它了解配置长什么样。**不要**为真实环境 fork 它。

你自己的用法：

1. 在你的组织或账号下 **新建** GitHub 仓库。
2. 把你自己的配置文件放进去（每个环境想要什么）。
3. 让 Grid 指向**那个**仓库 — 而不是 `grid-config`。

可以从示例里借鉴想法；仓库和设置归你所有。

## 仓库

| 仓库 | 用途 |
|------------|---------------|
| [grid-core](https://github.com/gridplatform/grid-core) | 在你的机器上运行 Grid — 背后的引擎，以及如何安装 |
| [grid-ui](https://github.com/gridplatform/grid-ui) | 你在浏览器里用的网站 |
| [grid-cli](https://github.com/gridplatform/grid-cli) | 同样的工作，在终端里完成，不必打开网站 |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | 常见云资源的现成积木（网络、服务器等） |
| [grid-config](https://github.com/gridplatform/grid-config) | 用来学习的示例配置 — **不是**你的真实环境（请自建仓库） |
| [grid-docs](https://github.com/gridplatform/grid-docs) | 通俗易懂的指南 |

完成 / 进行中 / 计划：**[STATUS.md](../../STATUS.md)**。

## 文档

| 指南 | 链接 |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## 贡献

Fork **产品**仓库（core、ui、cli、terraform、docs）→ 分支 → 向 `main` 提 PR。  
不要把 `grid-config` 当作你的私有期望状态仓库。

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

问题反馈：[grid-core](https://github.com/gridplatform/grid-core/issues)。

## 许可证

[MIT](../../LICENSE) © 2026 Grid Platform。

各产品仓库（grid-core、grid-ui、grid-cli 等）在相同条款下各自带有 `LICENSE`。
