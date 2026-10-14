<div align="center">

[English](../../profile/README.md) · [简体中文](README_zh.md) · [繁體中文](README_zh-TW.md) · [日本語](README_ja.md) · **한국어** · [Türkçe](README_tr.md) · [Русский](README_ru.md) · [Tiếng Việt](README_vi.md) · [ไทย](README_th.md) · [Deutsch](README_de.md) · [Español](README_es.md) · [Français](README_fr.md) · [Українська](README_uk.md) · [Polski](README_pl.md) · [Português (Brasil)](README_pt-BR.md) · [العربية](README_ar.md) · [فارسی](README_fa.md) · [Bahasa Indonesia](README_id.md) · [Italiano](README_it.md)

# Grid Platform

### 셀프호스팅 인프라 오케스트레이션 — desired-state JSON, Terraform 모듈, 감사 가능한 릴리스.

**당신의 컨트롤 플레인. 당신의 자격 증명. 당신의 상태.**

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Docs](https://img.shields.io/badge/docs-grid--docs-0A66C2?style=flat-square)](https://github.com/gridplatform/grid-docs)
[![Website](https://img.shields.io/badge/website-gridplatform.org-111111?style=flat-square)](https://gridplatform.org)
[![Status](https://img.shields.io/badge/status-living-2ea44f?style=flat-square)](../../STATUS.md)

**[Website](https://gridplatform.org) · [Docs](https://github.com/gridplatform/grid-docs) · [Status](../../STATUS.md)**

[빠른 시작](#빠른-시작) · [동작 방식](#동작-방식) · [당신의 desired state](#당신의-desired-state) · [저장소](#저장소) · [문서](#문서)

```bash
curl -fsSL https://raw.githubusercontent.com/gridplatform/grid-core/main/install/install.sh | sudo -E bash
```

![Grid Banner](../../readme-assets/banner.png)

</div>

---

Grid는 경로형 인프라 JSON을 공개 모듈 뱅크를 통해 Terraform으로 바꾸고, 감사 가능한 **release**로 **plan / apply / destroy**를 실행하며 GitOps 스타일 콘솔을 제공합니다. VM 또는 Docker Compose로 셀프호스트 — 벤더 종속성 없음, 순수 Terraform으로 이탈 가능.

> **데모 영상** — 곧 공개.

## 빠른 시작

1. **[원격 Terraform 상태](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md)** 생성 (S3 / GCS / Azure).
2. VM에 Grid 설치 (기본 Compose).

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

`http://<host>/` 열기. 장기 클라우드 키보다 VM의 **인스턴스 역할 / 서비스 계정**을 권장.

전체 경로: **[VM에 설치](https://github.com/gridplatform/grid-docs/blob/main/docs/install/vm.md)**.

## 동작 방식

| 구성 | 역할 |
|-------|------|
| **당신의** desired-state 저장소 | 직접 만든 GitHub 저장소 — 배포할 JSON |
| 모듈 뱅크 | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| grid-cli | Generate → plan → apply → destroy |
| grid-core | API, GitOps 동기화, 릴리스 + 실시간 로그 |
| grid-ui | 콘솔 |

클라우드 권한은 **호스트 ID**(AWS 인스턴스 역할 / GCP ADC)에서 옵니다. desired-state 파일에 자격 증명을 넣지 않습니다. 프로덕션은 원격 상태를 사용해 VM을 교체해도 Terraform 맵을 잃지 않습니다.

## 당신의 desired state

**[grid-config](https://github.com/gridplatform/grid-config)는 예시일 뿐입니다.** JSON 형태를 배우려면 읽으세요. 프로덕션용으로 **fork 하지 마세요**.

실제 배포 시:

1. 조직/계정에 **새** GitHub 저장소를 만듭니다.
2. 자신의 경로형 JSON을 추가합니다 (provider / env / 리소스 단위).
3. Grid를 그 저장소로 가리킵니다 (`GRID_GITOPS_REPO_URL`) — `grid-config`가 아닙니다.

예시에서 패턴을 복사하고, 저장소와 설정은 직접 소유하세요.

## 저장소

| Repo | 역할 |
|------|------|
| [grid-core](https://github.com/gridplatform/grid-core) | API + install (Compose, `install.sh`) |
| [grid-ui](https://github.com/gridplatform/grid-ui) | 콘솔 |
| [grid-cli](https://github.com/gridplatform/grid-cli) | Generate → plan → apply → destroy |
| [grid-terraform](https://github.com/gridplatform/grid-terraform) | Terraform modules ([grid-terraform](https://github.com/gridplatform/grid-terraform)) |
| [grid-config](https://github.com/gridplatform/grid-config) | **예시** desired-state (프로덕션 fork 아님) |
| [grid-docs](https://github.com/gridplatform/grid-docs) | 문서 |

완료 / 진행 중 / 계획: **[STATUS.md](../../STATUS.md)**.

## 문서

| 가이드 | 링크 |
|-------|------|
| Org adoption | [organizations.md](https://github.com/gridplatform/grid-docs/blob/main/docs/organizations.md) |
| Remote state | [remote-state.md](https://github.com/gridplatform/grid-docs/blob/main/docs/install/remote-state.md) |
| Install (VM / Compose) | [install/](https://github.com/gridplatform/grid-docs/tree/main/docs/install) |
| CLI (AWS / GCP) | [aws-gcp.md](https://github.com/gridplatform/grid-docs/blob/main/docs/cli/aws-gcp.md) |
| Concepts | [concepts/overview.md](https://github.com/gridplatform/grid-docs/blob/main/docs/concepts/overview.md) |

## 기여

**제품** 저장소(core, ui, cli, terraform, docs)를 fork → 브랜치 → `main`에 PR.  
`grid-config`를 개인 desired-state 저장소로 쓰지 마세요.

See [grid-docs CONTRIBUTING](https://github.com/gridplatform/grid-docs/blob/main/CONTRIBUTING.md).

이슈: [grid-core](https://github.com/gridplatform/grid-core/issues).

## 라이선스

MIT — see each repository’s `LICENSE`.
