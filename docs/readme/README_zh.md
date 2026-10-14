<div align="center">

[English](../../profile/README.md) · **简体中文** · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · [한국어](README_ko.md) · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### 自托管基础设施编排 — 期望状态 JSON、Terraform 模块、可审计发布。

**你的控制平面。你的凭证。你的状态。**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[快速开始](#快速开始) · [工作原理](#工作原理) · [你的期望状态](#你的期望状态) · [仓库](#仓库) · [文档](#文档)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid 将路径形基础设施 JSON 通过公共模块库转为 Terraform，以可审计的 **release** 运行 **plan / apply / destroy**，并提供 GitOps 风格控制台。在 VM 或 Docker Compose 上自托管 — 无厂商锁定，可走纯 Terraform 退出路径。

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

| 组件 | 作用 |
|-------|------|
| **你的**期望状态仓库 | 你自己创建的 GitHub 仓库 — 存放要部署的 JSON |
| 模块库 | Terraform 模块（[grid-terraform](https://github.com/gridplatform/grid-terraform)） |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API、GitOps 同步、release + 实时日志 |
| grid-ui | 控制台 |

云权限来自 **主机身份**（AWS 实例角色 / GCP ADC）。期望状态文件不携带凭证。生产环境使用远程状态，更换 VM 也不会丢失 Terraform 映射。

## 你的期望状态

**[grid-config](https://github.com/gridplatform/grid-config) 仅作示例。** 阅读它以了解 JSON 结构。**不要**为生产环境 fork 它。

对于真实部署：

1. 在你的组织或账号下 **新建** GitHub 仓库。
2. 写入你自己的路径形 JSON（provider / env / 资源单元）。
3. 让 Grid 指向该仓库（`GRID_GITOPS_REPO_URL`）— 而不是 `grid-config`。

从示例复制模式；仓库和配置归你所有。

## 仓库

| 仓库 | 作用 |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | 控制台 |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform 模块（[grid-terraform](https://github.com/gridplatform/grid-terraform)） |
| [grid-config](https://github.com/gridplatform/grid-config) | **示例**期望状态（不是你的生产 fork） |
| [grid-docs](https://github.com/gridplatform/grid-docs) | 文档 |

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

MIT — 见各仓库的 `LICENSE`。
