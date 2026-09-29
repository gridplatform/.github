<!-- # Grid Platform -->

![Grid Banner](../readme-assets/banner.png)

> **Infrastructure Orchestration Platform**  
> **Open-source, self-hosted alternative to expensive proprietary tools** - Complete control over your cloud infrastructure without vendor lock-in.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/gridplatform/grid-core?style=social)](https://github.com/gridplatform/grid-core)
[![Discord](https://img.shields.io/discord/1234567890?color=7289da&logo=discord&logoColor=white)](https://discord.gg/gridplatform)
<!-- [![CNCF](https://img.shields.io/badge/CNCF-Sandbox-blue)](https://www.cncf.io/) -->

## 🚀 What is Grid Platform?

Grid Platform is an open-source Infrastructure Orchestration Platform that solves the problem of expensive, vendor-locked infrastructure management tools. Built for solo DevOps engineers and mid-market companies who need enterprise-grade capabilities without the enterprise price tag.

**Key Benefits:**
- **🚫 No Vendor Lock-in** - Own your infrastructure code
- **💰 Free Forever** - No $50k-200k/year licensing fees
- **🔒 Self-Hosted** - Complete data sovereignty
- **☸️ Kubernetes Native** - Cloud-native architecture
- **🔄 GitOps First** - Built for modern DevOps workflows

## 🏗️ Repository Overview

| Repository | Purpose | Status |
|------------|---------|--------|
| [grid-core](https://github.com/gridplatform/grid-core) | Backend API (Node.js/TypeScript) | 🚧 In Development |
| [grid-ui](https://github.com/gridplatform/grid-ui) | Frontend Interface (React/TypeScript) | 🚧 In Development |
| [grid-cli](https://github.com/gridplatform/grid-cli) | CLI — JSON → Terraform generate / plan / deploy | 🚧 In Development |
| [grid-config](https://github.com/gridplatform/grid-config) | Desired-state GitOps JSON + `archive/` | 🚧 In Development |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Infrastructure Modules (Terraform) | 🚧 In Development |
| [grid-operator](https://github.com/gridplatform/grid-operator) | Kubernetes Operator (Go) | 🚧 In Development |
| [grid-ml](https://github.com/gridplatform/grid-ml) | AI/ML Features (Python) | 🚧 In Development |
| [grid-docs](https://github.com/gridplatform/grid-docs) | Documentation (Docusaurus) | 🚧 In Development |
<!-- | [gridplatform.org](https://github.com/gridplatform/gridplatform.org) | Website (Next.js) | 🚧 In Development | -->

## 🚀 Quick Start

Self-host on a VM or with Docker Compose — guides live in **grid-docs** (not this org profile repo):

- **[Install overview](https://github.com/gridplatform/grid-docs/blob/main/docs/install/overview.md)**
- **[Install on a VM](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**
- **[Docker Compose](https://github.com/gridplatform/grid-docs/blob/main/docs/install/docker-compose.md)**

Local API hack loop:

```bash
git clone https://github.com/gridplatform/grid-core.git
cd grid-core
npm install
npm run dev
```

## 📚 Learn More

- **📖 [Documentation](https://github.com/gridplatform/grid-docs)** — install, concepts, admin, CLI (`docs/`)
- **🌐 [Website](https://gridplatform.org)** - Learn more about Grid Platform
- **💬 [Discord Community](https://discord.gg/gridplatform)** - Get help and connect with users
- **🐛 [Report Issues](https://github.com/gridplatform/grid-core/issues)** - Found a bug? Let us know!

## 🤝 Contributing

We welcome contributions! See our [Contributing Guide](https://github.com/gridplatform/grid-core/blob/main/CONTRIBUTING.md) for details.

---

**Built with ❤️ by the open-source community**